This is a distribution repository for `bower` and `npm`. The sources for this repository are maintained at the [cloudinary_js repository](https://github.com/cloudinary/cloudinary_js). Please submit issues and pull requests to that repository.

# Cloudinary - bower and npm repository

Cloudinary is a cloud service that offers a solution to a web application's entire image management pipeline.

Easily upload images to the cloud. Automatically perform smart image resizing, cropping and conversion without installing any complex software. Integrate Facebook or Twitter profile image extraction in a snap, in any dimension and style to match your website’s graphics requirements. Images are seamlessly delivered through a fast CDN, and much much more.

Cloudinary offers comprehensive APIs and administration capabilities and is easy to integrate with any web application, existing or new.

Cloudinary provides URL and HTTP based APIs that can be easily integrated with any Web development framework.

## Getting started guide

![](http://res.cloudinary.com/cloudinary/image/upload/see_more_bullet.png)  **Take a look at our [Getting started guide for jQuery](http://cloudinary.com/documentation/jquery_integration#getting_started_guide)**. (Core JavaScript documentation coming soon.)


## Installation

### bower
1. Install the files using the following command. Use the optional `--save` parameter if you wish to save the dependency in your bower.json file.
  ```shell
  bower install cloudinary
  ```
1. Include the javascript file in your HTML. For Example:

  ```html
  <script src="../bower_components/cloudinary/cloudinary.js"></script>
  ```

## Setup

In order to properly use this library you have to provide it with a few configuration parameters:

Required:

* `cloud_name` - The cloudinary cloud name associated with your Cloudinary account.

Optional:

* `private_cdn`, `secure_distribution`, `cname`, `cdn_subdomain` - Please refer to [Cloudinary Documentation](http://cloudinary.com/documentation/rails_additional_topics#configuration_options) for information on these parameters.

To set these configuration parameters use the `Cloudinary::config` function (see below).

## Usage

The following blog post details the process of setting up a jQuery based file upload.
http://cloudinary.com/blog/direct_image_uploads_from_the_browser_to_the_cloud_with_jquery

The Cloudinary Documentation can be found at:
http://cloudinary.com/documentation

### Core JavaScript library

The Core Cloudinary JavaScript library provides several classes, defined under the "`cloudinary`" domain. The reference documentation is located at https://cloudinary.github.io/bower-cloudinary

#### Configuration

Start by instantiating a new Cloudinary class:

##### Explicitly

```javascript
var cl = cloudinary.Cloudinary.new( { cloud_name: "demo"});
```

##### Using the config function

```javascript

// Using the config function
var cl = cloudinary.Cloudinary.new();
cl.config( "cloud_name", "demo");
```

##### From meta tags in the current HTML document

When using the library in a browser environment, you can use meta tags to define the configuration options.

The `init()` function is a convenience function that invokes both `fromDocument()` and `fromEnvironment()`.


For example, add the following to the header tag:
```html
<meta name="cloudinary_cloud_name" content="demo">
```

In your JavaScript source, invoke `fromDocument()`:
```javascript
var cl = cloudinary.Cloudinary.new();
cl.fromDocument();
// or
cl.init();
```

##### From environment variables

When using the library in a backend environment such as NodeJS, you can use an environment variable to define the configuration options.

Set the environment variable, for example:
```shell
export CLOUDINARY_URL=cloudinary://demo
```
In your JavaScript source, invoke `fromEnvironment()`:
```javascript
var cl = cloudinary.Cloudinary.new();
cl.fromEnvironment();
// or
cl.init();

```

#### URL generation

```javascript
cl.url("sample")
// "http://res.cloudinary.com/demo/image/upload/sample"
cl.url( "sample", { width: 100, crop: "fit"})
// "http://res.cloudinary.com/demo/image/upload/c_fit,w_100/sample"

```

#### HTML tag generation

You can generate HTML tags in several ways:

`Cloudinary::image()` generates a DOM tag, and prepares it for responsive functionality. This is the same functionality as `$.cloudinary.image()` in the Cloudinary jQuery library.

```javascript
cl.image("sample")
```
produces:
```html
<img src=​"http:​/​/​res.cloudinary.com/​demo/​image/​upload/​sample" data-src-cache=​"http:​/​/​res.cloudinary.com/​demo/​image/​upload/​sample">​
```

You can generate an image Tag using the `imageTag` function:

```javascript
var tag = cl.imageTag("sample");
tag.toHtml();
```
which produces:
```html
<img src="http://res.cloudinary.com/demo/image/upload/sample">
```
and:
```javascript
tag.transformation().crop("fit").width(100).toHtml();
```
which produces:
```html
<img src="http://res.cloudinary.com/demo/image/upload/c_fit,w_100/sample">
```

You can also use `ImageTag` independently:

```javascript
var tag = cloudinary.ImageTag.new( "sample", { cloud_name: "some_other_cloud" });
tag.toHtml();
```
which produces:
```html
<img src="http://res.cloudinary.com/some_other_cloud/image/upload/sample">
```


#### Transformation

In addition to using a plain object to define transformations or using the builder methods (both described above), you can define transformations by using the Transformation class:

```javascript
var tr = cloudinary.Transformation.new();
tr.crop("fit").width(100);
tr.serialize()
// "c_fit,w_100"
```

You can also chain transformations together:

```javascript
var tr = cloudinary.Transformation.new();
tr.width(10).crop('fit').chain().angle(15).serialize()
// "c_fit,w_10/a_15"
```

![](http://res.cloudinary.com/cloudinary/image/upload/see_more_bullet.png) **See [our documentation](http://cloudinary.com/documentation/jquery_image_manipulation) for more information about displaying and transforming images using jQuery**.                                         

### Other Cloudinary JavaScript libraries

#### jQuery plugin
If you are using jQuery, you can take advantage of the Cloudinary jQuery plugin at https://github.com/cloudinary/bower-cloudinary-jquery.

#### jQuery File upload
The Cloudinary jQuery File Upload library extends the Cloudinary jQuery plugin that utilizes the [Blueimp jQuery File Upload library](https://blueimp.github.io/jQuery-File-Upload/).

## Additional resources

Additional resources are available at:

* [Website](http://cloudinary.com)
* [Documentation](http://cloudinary.com/documentation)
* [Knowledge Base](http://support.cloudinary.com/forums)
* [Documentation for jQuery integration](http://cloudinary.com/documentation/jquery_integration)
* [jQuery image upload documentation](http://cloudinary.com/documentation/jquery_image_upload)
* [jQuery image manipulation documentation](http://cloudinary.com/documentation/jquery_image_manipulation)
* [Image transformations documentation](http://cloudinary.com/documentation/image_transformations)

## Support

You can [open an issue through GitHub](https://github.com/cloudinary/cloudinary_js/issues).

Contact us at [http://cloudinary.com/contact](http://cloudinary.com/contact).

Stay tuned for updates, tips and tutorials: [Blog](http://cloudinary.com/blog), [Twitter](https://twitter.com/cloudinary), [Facebook](http://www.facebook.com/Cloudinary).


## License

Released under the MIT license.
