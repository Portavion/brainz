# Tmuxinator Templates
## Fullstack App
```yaml
# /Users/portavion/.config/tmuxinator/CodingChallenge.yml

name: CodingChallenge
root: ~/repos/FullStackEngineerCodingChallenge

windows:
  - Client:
      root: ~/repos/FullStackEngineerCodingChallenge/client
      panes:
        - nvim .
  - Server:
      root: ~/repos/FullStackEngineerCodingChallenge/server
      panes:
        - nvim .
  - logs:
      layout: main-vertical
      panes:
        - commands:
            - cd ~/repos/FullStackEngineerCodingChallenge/client
            - clear
            - npm run dev
        - commands:
            - cd ~/repos/FullStackEngineerCodingChallenge/server
            - source env/bin/activate
            - clear
            - uvicorn app.__main__:app --reload

```