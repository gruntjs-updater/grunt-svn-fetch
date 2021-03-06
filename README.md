# grunt-svn-fetch-cred

> Ensures specified files are checked out or updated from SVN repository.

## Getting Started
This plugin requires Grunt `~0.4.0`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

	npm install grunt-svn-fetch-cred --save-dev

One the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

	grunt.loadNpmTasks('grunt-svn-fetch-cred');

## The "svn_fetch" task

### Overview
This is a fork from https://www.npmjs.org/package/grunt-svn-fetch allowing you to also enter a username and password into the options

In your project's Gruntfile, add a section named `svn_fetch` to the data object passed into `grunt.initConfig()`.

	grunt.initConfig({
		svn_fetch: {
			options: {
				// Task-specific options go here.
			},
			your_target: {
				options: {
					// Target-specific settings and/or options go here.
				}
			},
		},
	})

The task works by checking for the presence of the ```.svn``` folder under each of the target folders. If present, an update is performed, otherwise a checkout is done.

### Options

#### options.bin
Type: `String`

Default value: `'svn'`

Specifies the location of the SVN binary.

#### options.execOptions
Type: 'Object'

Default value: `{}`

Specifies any options to pass to the `exec` command when executing the svn cli statements. For example, it may be necessary to increase the default `maxBuffer` for larger repositories.

#### options.username
Type: `String`

Default value: none

The username of the SVN repository. Username and password will not be used unless both options are used

#### options.password
Type: `String`

Default value: none

The password of the SVN repository. Username and password will not be used unless both options are used

#### options.repository
Type: `String`

Default value: `''`

The URL of the SVN repository.

#### options.path
Type: `String`

Default value: `''`

The base element of the path to where checked out or updated files are placed.

### Usage Examples

	grunt.initConfig({
		svn_fetch: {
			options: {
				'repository':	'https://my_repos.com/projectX/trunk/',
				'path': 		'/svn/projectX/src/',
				'username': 'svnUsername',
				'password': 'svnPassword'
			},
			projectX: {
	    		map: {
			    	'folderX': 'SVNFolderX',
					'folderY': 'SVNFolderY'
				}
			}
	    },
	});

Each entry in ```map``` utilises the ```path``` and ```respository``` options to determine the full path and URL of the items being considered. So, in this case, the first entry would resolve to:

	/svn/projectX/src/folderX

and

	https://my_repos.com/projectX/trunk/SVNFolderX

Note the inclusion of slashes on the option entries. The plugin makes no effort to ensure slashes are correct.

## Release History
* 2013-03-13 0.1.0 Initial release
* 2013-03-13 0.1.2 Issue #1 fixed
* 2013-12-11 0.1.3 Issue #2 fixed
