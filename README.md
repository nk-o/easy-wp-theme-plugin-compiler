# 🤪 WPEG - WP Easy Generator

## 🤓 Installation

```$ npm install wpeg --save-dev```

## 🤓 Prepare config

WPEG works only with config in your theme/plugin directory. Create file `wpeg.config.js`. Example of file config used in our [Lazy Blocks](https://github.com/nk-o/lazy-blocks) plugins:

```javascript
const pkg = require( 'json-file' ).read( './package.json' ).data;

const cfg = {};

// Build Paths.
cfg.name = 'lazy-blocks';
cfg.src = './src';
cfg.dist_root = './dist';
cfg.dist = '{dist_root}/{name}';

// Template variables that will be automatically replaced.
cfg.template_files_src = '{src}/**/*.{php,js,css}';
cfg.template_files_variables = {
    text_domain: pkg.name,
    plugin_version: pkg.version,
    plugin_name: pkg.name,
    plugin_title: pkg.title,
    plugin_author: pkg.author,
};

// Copy files.
cfg.copy_files_src = [ '{src}/**/*', '!{src}/**/*.{js,jsx,scss}', '{src}/**/vendor/**/*.{js,jsx,scss}' ];

// Compile SCSS files.
cfg.compile_scss_files_src = [ '{src}/**/*.scss', '!{src}/**/vendor/**/*' ];

// Compile JS files.
cfg.compile_js_files_src = [ '{src}/**/*.js', '!{src}/**/vendor/**/*' ];

// Compile JSX files.
cfg.compile_jsx_files_src = [ '{src}/*assets/js/index.jsx', '{src}/*assets/admin/js/blocks.jsx' ];

// Correct line endings files.
cfg.correct_line_endings_files_src = '{dist}/**/*.{js,css}';

// Translate PHP files.
cfg.translate_php_files_src = '{dist}/**/*.php';
cfg.translate_php_files_dist = `{dist}/languages/${ cfg.template_files_variables.plugin_name }.pot`;
cfg.translate_php_options = {
    domain: cfg.template_files_variables.text_domain,
    package: cfg.template_files_variables.plugin_title,
    lastTranslator: cfg.template_files_variables.plugin_author,
    team: cfg.template_files_variables.plugin_author,
};

// ZIP files.
cfg.zip_files = [
    {
        src: '{dist}/**/*',
        dist: '{dist_root}/lazy-blocks.zip',
    },
];

// Browser Sync.
cfg.browser_sync = {
    proxy: '{name}.local',
    host: '{name}.local',
    open: 'external',
};

// Watch files.
cfg.watch_files = [ '{src}/**/*', '!{src}/**/*.{php,jsx,js,scss}' ];

cfg.watch_js_files = [ '{src}/**/*.js', '!{src}/*vendor/**/*' ];

cfg.watch_jsx_files = [ '{src}/**/*.jsx', '!{src}/*vendor/**/*' ];

cfg.watch_scss_files = '{src}/**/*.scss';

module.exports = cfg;
```

## 🤗 Usage

```$ npx wpeg <options>```

## 🤤 Options

- `-b`, `--build`     build theme/plugin
- `-w`, `--watch`     start watch changes in files and automatically run 'build' after changes
- `-z`, `--zip`       prepare ZIP file after build

## 🤫 Other options

- `--config`          custom config, by default used: `--config="wpeg.config.js"`
- `-h`, `--help`      show usage information
- `-v`, `--version`   show version info

## 😬 Example

```$ npx wpeg -b -w```
