```python
HTML_HEAD_PART_1 = """<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
"""
HTML_STYLE_START = "  <style>"
HTML_STYLE_CONTENT = """
    body {
        font-family: monospace, Consolas, Menlo, Monaco, 'Courier New', Courier;
        font-size: 14px;
        line-height: 1.4;
    }
    pre {
        margin: 0;
        padding: 0.2em 0.5em;
        white-space: pre-wrap;
        word-wrap: break-word;
        display: block;
        border: none;
        border-radius: 0;
    }
    pre.diff-add { background-color: #e6ffed; color: #24292e; }
    pre.diff-delete { background-color: #ffeef0; color: #24292e; }
    pre.diff-context { background-color: #f6f8fa; color: #586069; }
    pre.diff-info { background-color: #fffbdd; color: #586069; }
    pre.diff-header { background-color: #f1f8ff; color: #0366d6; font-weight: bold; }
"""
HTML_END_PART = """  </style>
</head>
<body>
<hr>
"""

HTML_FOOTER = """</body>
</html>"""

```