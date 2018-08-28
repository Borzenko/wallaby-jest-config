
```
/* eslint-disable */
module.exports = function () {
  return {
    files: [
      'folder/**/*.js',
      'folder/**/*.json',
      'anotherfolder/**/*js',
      '!anotherfolder/**/*test.js',
      '!folder/**/*test.js',
      'config/jest-global-setup.js',
      'config/jest-global-teardown.js',
      'config/jest-setup.js',
    ],

    tests: [
      'folder/**/*test.js',
      'anotherfolder/**/*test.js',
    ],

    env: {
      type: 'node',
      runner: 'node'
    },

    testFramework: 'jest',
    setup: function (wallaby) {
      const jestConfig = require('./package.json').jest;
      if (jestConfig.setupTestFrameworkScriptFile) {
          jestConfig.setupTestFrameworkScriptFile = jestConfig.setupTestFrameworkScriptFile.replace('<rootDir>', wallaby.projectCacheDir);
      }
      if (jestConfig.globalSetup) {
          jestConfig.globalSetup = jestConfig.globalSetup.replace('<rootDir>', wallaby.projectCacheDir);
      }
      if (jestConfig.globalTeardown) {
        jestConfig.globalTeardown = jestConfig.globalTeardown.replace('<rootDir>', wallaby.projectCacheDir);
      }
    },
  };
};
```
