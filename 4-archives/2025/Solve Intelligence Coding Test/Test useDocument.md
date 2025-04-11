```js
import { renderHook, act, waitFor } from "@testing-library/react";
import axios from "axios";
import { describe, it, expect, beforeEach, vi } from "vitest";

import { useDocument } from "./useDocument";
export interface ApiResponse {
  document_id: number;
  document_version: number;
  content: string;
  available_versions: number[];
}
vi.mock("axios");

const mockedAxios = vi.mocked(axios, true);

const BACKEND_URL = "http://localhost:8000";

const mockDoc1V1_Response: ApiResponse = {
  document_id: 1,
  document_version: 1,
  content: "Content for Patent 1 Version 1",
  available_versions: [1, 2],
};

const mockDoc1V2_Response: ApiResponse = {
  document_id: 1,
  document_version: 2,
  content: "Content for Patent 1 Version 2 - Updated",
  available_versions: [1, 2],
};

const mockDoc1V3_Saved_Response: ApiResponse = {
  document_id: 1,
  document_version: 3,
  content: "Newly Saved Content",
  available_versions: [1, 2, 3],
};

describe("useDocument Hook (with Vitest)", () => {
  beforeEach(() => {
    mockedAxios.get.mockClear();
    mockedAxios.post.mockClear();
  });

  describe("Initial Loading", () => {
    it("should load the initial document successfully", async () => {
      const initialId = 1;
      const expectedUrl = `${BACKEND_URL}/document/${initialId}`;

      mockedAxios.get.mockResolvedValue({ data: mockDoc1V1_Response });

      const { result } = renderHook(() => useDocument(initialId));

      expect(result.current.isLoading).toBe(true);

      await waitFor(() => expect(mockedAxios.get).toHaveBeenCalledTimes(1));
      expect(mockedAxios.get).toHaveBeenCalledWith(expectedUrl);

      await waitFor(() => expect(result.current.isLoading).toBe(false));

      expect(result.current.currentDocument).toEqual({
        id: mockDoc1V1_Response.document_id,
        currentVersion: mockDoc1V1_Response.document_version,
        content: mockDoc1V1_Response.content,
        availableVersions: mockDoc1V1_Response.available_versions,
      });
    });
  });

  describe("Saving with saveDocument", () => {
    async function setupLoadedDocument(hookResult: any) {
      const initialId = 1;
      mockedAxios.get.mockResolvedValue({ data: mockDoc1V1_Response });
      await act(async () => {
        await hookResult.current.loadDocument(initialId);
      });
      await waitFor(() => expect(hookResult.current.isLoading).toBe(false));
      await waitFor(() =>
        expect(hookResult.current.currentDocument).not.toBeNull(),
      );
      mockedAxios.get.mockClear();
    }

    it("should save updates to the current version successfully", async () => {
      const { result } = renderHook(() => useDocument());
      await setupLoadedDocument(result);

      const updatedContent = "Updated Content for V1";
      act(() => {
        result.current.handleContentChange(updatedContent);
      });

      const saveResponse = { ...mockDoc1V1_Response, content: updatedContent };
      const expectedUrl = `${BACKEND_URL}/save/${mockDoc1V1_Response.document_id}/${mockDoc1V1_Response.document_version}`;
      const expectedBody = { content: updatedContent };

      mockedAxios.post.mockResolvedValue({ data: saveResponse });

      await act(async () => {
        await result.current.saveDocument(false);
      });

      await waitFor(() => expect(mockedAxios.post).toHaveBeenCalledTimes(1));
      expect(mockedAxios.post).toHaveBeenCalledWith(expectedUrl, expectedBody);

      await waitFor(() => expect(result.current.isLoading).toBe(false));

      expect(result.current.currentDocument?.content).toBe(updatedContent);
      expect(result.current.currentDocument?.currentVersion).toBe(
        mockDoc1V1_Response.document_version,
      );
    });

    it("should save as a new version successfully", async () => {
      const { result } = renderHook(() => useDocument());
      await setupLoadedDocument(result);

      const newContent = "Newly Saved Content";
      act(() => {
        result.current.handleContentChange(newContent);
      });

      const expectedUrl = `${BACKEND_URL}/save/${mockDoc1V1_Response.document_id}`;
      const expectedBody = { content: newContent };

      mockedAxios.post.mockResolvedValue({ data: mockDoc1V3_Saved_Response });

      await act(async () => {
        await result.current.saveDocument(true);
      });

      await waitFor(() =>
        expect(mockedAxios.post).toHaveBeenCalledWith(
          expectedUrl,
          expectedBody,
        ),
      );
      await waitFor(() => expect(result.current.isLoading).toBe(false));

      expect(result.current.currentDocument?.currentVersion).toBe(
        mockDoc1V3_Saved_Response.document_version,
      );
      expect(result.current.currentDocument?.content).toBe(
        mockDoc1V3_Saved_Response.content,
      );
      expect(result.current.currentDocument?.availableVersions).toEqual(
        mockDoc1V3_Saved_Response.available_versions,
      );
    });
  });

  describe("State Update Handlers", () => {
    it("handleContentChange should update the content state immediately", async () => {
      const { result } = renderHook(() => useDocument());
      mockedAxios.get.mockResolvedValue({ data: mockDoc1V1_Response });
      await act(async () => {
        await result.current.loadDocument(1);
      });
      await waitFor(() =>
        expect(result.current.currentDocument).not.toBeNull(),
      );

      const newContent = "My typed content";
      act(() => {
        result.current.handleContentChange(newContent);
      });

      expect(result.current.currentDocument?.content).toBe(newContent);
      expect(mockedAxios.get).toHaveBeenCalledTimes(1);
      expect(mockedAxios.post).not.toHaveBeenCalled();
    });

    it("handleVersionChange should call loadDocument triggering a GET request", async () => {
      const { result } = renderHook(() => useDocument());
      mockedAxios.get.mockResolvedValueOnce({ data: mockDoc1V1_Response });
      await act(async () => {
        await result.current.loadDocument(1);
      });
      await waitFor(() => !!result.current.currentDocument);
      expect(mockedAxios.get).toHaveBeenCalledTimes(1);
      expect(mockedAxios.get).toHaveBeenCalledWith(`${BACKEND_URL}/document/1`);

      const expectedV2Url = `${BACKEND_URL}/document/1/2`;
      mockedAxios.get.mockResolvedValueOnce({ data: mockDoc1V2_Response });

      const mockEvent = {
        target: { value: "2" },
      } as React.ChangeEvent<HTMLSelectElement>;
      act(() => {
        result.current.handleVersionChange(mockEvent);
      });

      await waitFor(() => expect(mockedAxios.get).toHaveBeenCalledTimes(2));
      expect(mockedAxios.get).toHaveBeenCalledWith(expectedV2Url);

      await waitFor(() => expect(result.current.isLoading).toBe(false));
      expect(result.current.currentDocument?.currentVersion).toBe(
        mockDoc1V2_Response.document_version,
      );
      expect(result.current.currentDocument?.content).toBe(
        mockDoc1V2_Response.content,
      );
    });
  });
});

```