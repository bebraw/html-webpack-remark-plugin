# html-webpack-remark-plugin - Render Markdown to React through Remark

This is a plugin for [html-webpack-plugin](https://www.npmjs.com/package/html-webpack-plugin) that allows you to render Markdown through [remark](https://www.npmjs.com/package/remark) and [remark-react](https://www.npmjs.com/package/remark-react) and to inject it into **html-webpack-plugin** template context.

The advantage of doing this is that you'll get HTML out of the box (avoids `dangerouslySetInnerHTML`). This helps with SEO purposes and makes your page load a bit better.

## Usage

```javascript
import HtmlWebpackPlugin from 'html-webpack-plugin';
import HtmlWebpackRemarkPlugin from 'html-webpack-remark-plugin';

// Import custom programming languages for remark to process
import js from 'highlight.js/lib/languages/javascript';

const config = {
  plugins: [
    new HtmlWebpackPlugin({
      title: pkg.name + ' - ' + pkg.description,
      template: 'lib/index_template.ejs',
      inject: false,

      // Context for the template
      name: pkg.name,
      description: pkg.description,
      demonstration: RENDER_UNIVERSAL ? ReactDOM.renderToString(<App />) : ''
    }),
    new HtmlWebpackRemarkPlugin({
      // Key under which to inject the processed file
      key: 'documentation',

      // Markdown file to read and process
      file: path.join(__dirname, 'README.md'),

      // Custom programming languages to process
      languages: {
        js: js
      }
    }),
    ...
  ],
  ...
}
```

You can see the plugin in action at the [react-component-boilerplate](https://github.com/survivejs/react-component-boilerplate).

> Check out [SurviveJS - Webpack and React](http://survivejs.com/) to dig deeper into the topic.

## License

MIT.
