##### CSS 

```json
{
    "Basic CSS template": {
        "prefix": "!",
        "body": [
            ":root {",
            "$0",  
            "}",
            "",
            "html {",
            "    box-sizing: border-box;",
            "}",
            "",
            "*,",
            "*::before,",
            "*::after {",
            "    box-sizing: inherit;",
            "}"
        ],
        "description": "basic css styles"
    },
    
    "simple comment": {
        "prefix": "//",
        "body": [
            "/* $0 */"
        ]
    }
}
```

##### TSX

```json
{
"React Functional Component": {
        "prefix": "rfc",
        "body": [
            "import './${1: Stylesheet}';",
            "",
            "const ${2:ComponentName} = () => {",
            "",
            "  return (",
            "    <div>",
            "",
            "    </div>",
            "  );",
            "};",
            "",
            "export default ${3:ComponentName};"
        ],
        "description": "React Functional Component"
    },
}
```

