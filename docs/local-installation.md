## Local Installation

In browser environment, `tesseract.js` simply provides the API layer. Internally, it opens a WebWorker to handle requests. That worker itself loads code from the Emscripten-built `tesseract.js-core` which itself is hosted on a CDN. Then it dynamically loads language files hosted on another CDN.

Because of this we recommend loading `tesseract.js` from a CDN. But if you really need to have all your files local, you can pass extra arguments to `TessearctWorker` to specify custom paths for workers, languages, and core.

In Node.js environment, the only path you may want to customize is languages/langPath.

```javascript
const worker = Tesseract.TesseractWorker({
  workerPath: 'https://cdn.jsdelivr.net/gh/naptha/tesseract.js@v2.0.0-alpha.2/dist/worker.min.js',
  langPath: 'https://tessdata.projectnaptha.com/4.0.0',
  corePath: 'https://cdn.jsdelivr.net/gh/naptha/tesseract.js-core@v2.0.0-beta.5/tesseract-core.js',
});
```

### workerPath
A string specifying the location of the [worker.js](./dist/worker.min.js) file.

### langPath
A string specifying the location of the tesseract language files, with default value 'https://tessdata.projectnaptha.com/4.0.0'. Language file URLs are calculated according to the formula `langPath + langCode + '.traineddata.gz'`.

### corePath
A string specifying the location of the [tesseract.js-core library](https://github.com/naptha/tesseract.js-core), with default value 'https://cdn.jsdelivr.net/gh/naptha/tesseract.js-core@v2.0.0-beta.5/tesseract-core.js'.