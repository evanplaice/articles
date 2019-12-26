        

```json
"dependencies": {
  "@babel/cli": "^7.0.0-beta.39",
  "@babel/core": "^7.0.0-beta.39",
  "@babel/plugin-proposal-pipeline-operator": "^7.0.0-beta.39",
  "chokidar-cli": "^1.2.0"
}


```json
"scripts": {
  "start": "npx chokidar './src/*.js' -c 'npx babel ./src/$(basename {path}) 
  -o ./dist/$(basename {path})'"
}
```