https://survivejs.com/webpack/what-is-webpack/#resolution-process
- If the resolution pass failed, webpack raises a runtime error. If webpack managed to resolve a file correctly, webpack performs processing over the matched file based on the loader definition. Each loader applies a specific transformation against the module *contents*.
- The way a loader gets matched against a resolved file can be configured in multiple ways, including *by file type* and *by location* within the file system. Webpack's flexibility even allows you to apply a specific transformation to a file based on *where* it was imported into the project.

https://survivejs.com/webpack/what-is-webpack/#evaluation-process
- Assuming all loaders were found, webpack evaluates the matched loaders from bottom to top and right to left

Loaders can be chained. They are applied in a pipeline to the resource. A chain of loaders are executed in reverse order. The first loader in a chain of loaders returns a value to the next. At the end loader, webpack expects JavaScript to be returned.

- Loaders can be synchronous or asynchronous.
- Loaders run in Node.js and can do everything that’s possible there.
- Loaders can emit additional arbitrary files.

https://survivejs.com/webpack/styling/separating-css/
- `ExtractTextPlugin.extract` accepts `use` and `fallback` definitions. ExtractTextPlugin processes content through `use` only from initial chunks by default and it uses `fallback` for the rest. It doesn't touch any split bundles unless `allChunks: true` is set true. The Bundle Splitting chapter digs into greater detail.

...

Current chapter read: https://survivejs.com/webpack/loading/loader-definitions/