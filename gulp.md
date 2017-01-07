# gulp operation manual
> referances: [gulpjs official website](http://www.gulpjs.com.cn/docs/cli/) and [npm official web site](https://www.npmjs.com/package/gulp)

### gulp  commands cli

- <code>-v</code> or <code>--version</code> displays the gulp version number installed locally and global for the project
- <code>require  &lt;module path&gt;</code> will require a module before execution
- <code>gulpfile &lt;gulpfile path&gt;</code> manually specify a path to gulpfile, which is usefull when you have many gulp files
- <code>--cwd &lt;dir path&gt;</code> Specify CWD. Defines where gulpfile looks
- <code>-T</code> or <code>--tasks</code> displays the task dependency tree for the specified gulpfile
- <code>-tasks-simple</code> displays the list of tasks in the loaded gulpfile as plain text
- <code>--color</code> mandatory gulp and gulp plug-in display color, even if there is no color support
- <code>no-color</code> mandatory undisplay color, even if there is no color support
- <code>--silent</code> prohibit all gulp logs
- ##### the command line will record where it was run in process.env.INIT_CW

### Tasks
> Task can be gulp &lt;task&gt; &lt;othertask&gt; way to implement. If only the <code>gulp</code> command is run, the registered task named <code>default</code> will be executed. If there is no task, gulp will report error.

## gulp require dependency
- <code>"gulp"</code> obtain gulp
- <code>"gulp-changed"</code>
- <code>"gulp-uglify"</code> js unzip plug-in
- <code>"gulp-concat"</code> merge files
- <code>"gulp-imagemin"</code> picture unzip plug-in
- <code>"gulp-minify-css"</code> css unzip plug-in, but deprecated, use <cod>"gulp-clean-css"</code>
- <code>"gulp-clean-css"</code>
- <code>"gulp-html"</code>
- <code>"gulp-livereload"</code>
