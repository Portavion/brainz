```python
@app.websocket("/ws")
async def websocket(websocket: WebSocket, ai: AI = Depends(get_ai)):
    await websocket.accept()
    while True:
        try:
            """
            The AI doesn't expect to receive any HTML.
            You can call ai.review_document to receive suggestions from the LLM.
            Remember, the output from the LLM will not be deterministic, so you may want to validate the output before sending it to the client.
            """
            document = await websocket.receive_text()
            print("Received data via websocket")
            review_generator = ai.review_document(document)
            full_response = ""

            async for chunk in review_generator:
                if chunk is not None:
                    full_response += chunk

            try:
                if full_response:
                    json_response = json.loads(full_response)
                    print(json.dumps(json_response, indent=2))
                else:
                    print("No response received from the AI.")
            except json.JSONDecodeError:
                print("Received invalid JSON response:", full_response)

        except WebSocketDisconnect:
            break
        except Exception as e:
            print(f"Error occurred: {e}")
            continue

```
Response:
```json
{
  "issues": [
    {
      "type": "Punctuation",
      "severity": "medium",
      "paragraph": 1,
      "description": "The punctuation is incorrect. The claim does not use traditional punctuations.",
      "suggestion": "Revise the punctuation to use colons to separate the transitional phrase from the body, and use semicolons to separate the elements."
    },
    {
      "type": "Ambiguity and Indefinite Issues",
      "severity": "high",
      "paragraph": 1,
      "description": "The phrase 'the device comprising multiple optical windows for complex neural activity control' is vague and could lead to ambiguity.",
      "suggestion": "Specify the function or purpose of the optical windows for defining the subject matter and avoiding ambiguity."
    },
    {
      "type": "Broadening Dependent Claims",
      "severity": "high",
      "paragraph": 2,
      "description": "Dependent claim 2 seems to broaden the claim it depends on rather than narrowing it.",
      "suggestion": "Revise the dependent claim 2 to further narrow the scope of the wireless optogenetic device, in accordance with the main claim (claim 1)."
    }
  ]
}
```