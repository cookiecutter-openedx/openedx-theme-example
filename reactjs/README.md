# edX Theme Example -- ReactJS Hello World apps

Both subdirectories contained here were created using [Create React App](https://github.com/facebook/create-react-app). These are sample ReactJS apps that, if you prefer, can be managed independently of this edX custom theme repository.

Please note the following:

* The custom Mako template file [add-react.html](../lms/templates/add-react.html) conditionally adds the necessary ReactJS library files that bring life to these two ReactJS apps.
* add-react.html will load the ReactJS libraries iff it finds a custom css class named 'reactjs-app' in the DOM. This is a custom convention that I invented for the sole purpose of limiting the ReactJS overhead to pages in the Open edX platform that actually include ReactJS apps.
* This implementation of ReactJS depends on [Babel](https://babeljs.io/) to transpile the ReactJS source code in this repository at run-time rather than creating js bundles via an actual JS build pipeline. This is not a requirement. There are many ways to deploy ReactJS apps. Use the approach that works best for your project. If your ReactJS app become suitable large then you might want to consider changing to the more traditional ReactJS production bundle.
