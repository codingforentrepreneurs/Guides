# Install Frameworks with Cocoapods

Cocoapods is a "CocoaPods is the dependency manager for Swift and Objective-C Cocoa projects. It has almost ten thousand libraries and can help you scale your projects elegantly."



## Step-by-Step Guide


1. Confirm RubyGems installed:
	
	`$ gem -v`
	
	Errors? Download and install here: [https://rubygems.org/pages/download](https://rubygems.org/pages/download)

2. Update the gems:

	`$ sudo gem update --system`

3. Install Cocoapods:

	`$ sudo gem install cocoapods`

	*Above command also updates cocoapods

4. Create Xcode Project:

	`Applications > Xcode > File > New > Project`

	Save it in a location of your choice. Such as:

	`Desktop > Development > you_project`
	
	After you save it, you'll find:
	
	`YourProject > YourProject.xcodeproj`
	
	Your new project path is: `Desktop/Development/you_project/YourProject/YourProject.xcodeproj`

5. Create a `Podfile`:
	
	Locate project's root path: 
	
	`Desktop/Development/you_project/`
	
	Then:
	
	`$ nano Podfile`
	
	Add the follwing to the `Podfile`:
	
	```
	xcodeproj 'YourProject/YourProject.xcodeproj'

	source 'https://github.com/CocoaPods/Specs.git'
	platform :ios, '8.0'
	use_frameworks!


	target 'test' do
	    pod 'SwiftyJSON', '~> 2.2.0'
	    pod 'Alamofire', '1.2'
	    #any other frameworks you want to use
	end
	```
	
	Save and close.

6. Install Pod:
	
	`$ pod install`
	
	If errors run the following:
	
	`$ rm -rf ~/.cocoapods`
	
	`$ pod setup`
	
	`$ pod install`
	
7. Now you should have a file called `YourProject.xcworkspace` in `Desktop/Development/you_project/`. This will be **the project you work with** from now on.

8. Add your frameworks to `Linked Frameworks and Libraries` in your Xcode Project's settings. 






Subscribe on our [YouTube Channel](http://joincfe.com/youtube) and join us for more in-depth tutorials on [Django development](http://joincfe.com/enroll).


Cheers!


#### Organized by CodingForEntrepreneurs