![ObjectiveKit - Swift friendly ObjC-Runtime functions ](https://cloud.githubusercontent.com/assets/889949/20255787/af3dced6-aa3f-11e6-9abb-f7b4a250f25c.png)


[![Build Status](https://travis-ci.org/marmelroy/ObjectiveKit.svg?branch=master)](https://travis-ci.org/marmelroy/ObjectiveKit)
[![Version](http://img.shields.io/cocoapods/v/ObjectiveKit.svg)](http://cocoapods.org/?q=ObjectiveKit)
[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)

# ObjectiveKit
ObjectiveKit provides a Swift-friendly API for a set of powerful Objective C runtime functions.

## Usage

To use ObjectiveKit:

Import ObjectiveKit at the top of your Swift file.

```swift
import ObjectiveKit
```

To access the functionality of ObjectiveKit you will need to create an ObjectiveClass object typed for the class you want to modify or introspect:

```swift
let viewClass = ObjectiveClass<UIView>()
```

If using for a custom Swift class, make sure that it inherits at some point from NSObject and that it is exposed to the Objective C runtime using the @objc flag.

### Introspection

You can learn more about classes at runtime with these handy introspection methods:
```swift
let mapViewClass = ObjectiveClass<MKMapView>()
let selectors = mapViewClass.allSelectors() // Returns an array of selectors.
let properties = mapViewClass.allProperties() // Returns an array of properties.
let protocols = mapViewClass.allProtocols() // Returns an array of protocols.
```

### Modifying classes at runtime

ObjectiveKit to add / exchange methods for a class at runtime.

You can add a pre-existing function from another class to your Objective class:
```swift
let viewClass = ObjectiveClass<UIView>()
viewClass.addSelectorToClass(#selector(testSelector), fromClass: self.classForCoder)
let view = UIView()
view.perform(#selector(testSelector))
```

Alternatively, you can add a method by providing a custom implementation with a closure:
```swift
let viewClass = ObjectiveClass<UIView>()
viewClass.addMethodToClass(closureName, implementation: {
    print("hello world")
})
let view = UIView()
view.performMethod(closureName)
```

ObjectiveKit also supports exchanging selectors in the same class:
```swift
let viewClass = ObjectiveClass<UIView>()
viewClass.exchangeSelector(#selector(UIView.layoutSubviews), with: #selector(UIView.xxx_layoutSubviews))
```

## Setting up

### Setting up with [CocoaPods](http://cocoapods.org/?q=ObjectiveKit)
```ruby
source 'https://github.com/CocoaPods/Specs.git'
pod 'ObjectiveKit', '~> 0.1'
```

### Setting up with Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager that automates the process of adding frameworks to your Cocoa application.

You can install Carthage with [Homebrew](http://brew.sh/) using the following command:

```bash
$ brew update
$ brew install carthage
```

To integrate Interpolate into your Xcode project using Carthage, specify it in your `Cartfile`:

```ogdl
github "marmelroy/ObjectiveKit"
```

### Inspiration
- [https://github.com/mikeash/MAObjCRuntime](https://github.com/mikeash/MAObjCRuntime)
