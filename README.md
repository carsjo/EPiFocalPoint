#Focal point based cropping for EPiServer using ImageResizing.NET

##Prerequisites
Make sure your Image Media ContentTypes inherit from ```ImageResizer.Plugins.EPiFocalPoint.FocalPointImageData```, or implements ```ImageResizer.Plugins.EPiFocalPoint.IFocalPointData``` if inheritance is inconvenient or undesired. Remember to decorate the FocalPoint property with ```[BackingType(typeof(PropertyFocalPoint))]``` if you choose to implement the interface only.

Creating NuGet packages requires Visual Studio 2015.

##Usage
Edit the image in AllPropertiesView, and place the red dot where you want it in the image.

##What is installed?
1. An ImageResizing.NET plugin is installed in web.config

		<resizer>
			<plugins>
				<add name="EPiFocalPointPlugin" />
			</plugins>
		</resizer>

1. ClientResources are installed (the editor needed for editors to place the focal point), along with some dojo stuff in module.config

		<module>
			<dojo>
				<paths>
					<add name="focal-point" path="" />
				</paths>
			</dojo>
		</module>


##How it works
The coordinates of the focal point are stored as a ```ImageResizer.Plugins.EPiFocalPoint.SpecializedProperties.FocalPoint``` property on the image. 
The image dimensions are also stored in the properties ```OriginalWidth``` and ```OriginalHeight``` whenever the image is saved.

When the image is requested, the ```crop``` parameter is added "under the hood", and then ImageResizing does its thing.

##Additional localizations
Embedded localizations are provided for Swedish and English. Should you need to localize in other languages, you can do so by adding XML translations thusly:

		<contenttypes>
			<imagedata>
				<properties>
					<focalpoint>
						<caption>Focal point</caption>
						<help>The point in the image, where the focus should be, automatically cropped images will be calculated based on this point.</help>
					</focalpoint>
					<originalheight>
						<caption>Height</caption>
						<help>The image height in pixels.</help>
					</originalheight>
					<originalwidth>
						<caption>Width</caption>
						<help>The image width in pixels.</help>
					</originalwidth>
				</properties>
			</imagedata>
		</contenttypes>

## Release history

### Release 1.0.0
Initial release.

### Release 1.1.0
1. Added clear button to remove a focal point in an image
2. Style changes to show the focal point as greyed out if the image doesn't have any focal point set
3. Changed the ClientEditingClass from dot notation to use Dojo AMD notation.

### Release 1.1.1
1. Added support for .NET 4.6 and 4.5.2
2. Updated module.config to be created if not existing in target project

### Release 1.2.0
1. Added an interface if inheritance isn't an option.
2. Added support for CMS 10.

### Release 1.2.1
1. Fixes issue when generating cache keys.
2. FIxes issue with initialization of localization provider.

### Release 1.3.0
1. Optimized reading of image dimensions for faster processing of image data.