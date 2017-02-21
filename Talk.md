![fit inline](logo-cocoa-heads.gif)

# CocoaHeads CPS

## *Francesco Perrotti-Garcia*

---

#[fit] Caterpillar_: de ideia a publicação_

#[fit] **criando seus próprios frameworks**

---

![left](gravatar.jpg)
#[fit] *Francesco* 
#[fit] *Perrotti-Garcia*
#[fit] iOS Developer
#[fit] **_@fpg1503_**

---

#[fit] Frameworks

---

#[fit] >> 🙋🙋‍♂️ <<

---

#[fit] *Usou um*
#[fit] gerenciador
#[fit] de 
#[fit] **dependências?**

---

![fit](logo-cocoapods.png)

---

![fit](logo-carthage.png)

---

![fit](logo-swift.png)

---

#[fit] *Publicou*
#[fit] um 
#[fit] **framework?**

---

#[fit] >> 📚 << 

---

#[fit] >> 🐛 << 

---

#[fit] >> 💡 <<

---

#[fit] `dd/mm/yyyy`

---

#[fit] 21/08/2017

---

#[fit] 21/02/2017
#[fit] 21h08

---

#[fit] 21/_02_/2017
#[fit] _21h_08

---

#[fit] `mm`
#[fit] minutos

---

#[fit] `MM`
#[fit] mês

---

#[fit] `yyyy-MM-dd'T'HH:mm:ssZ`

---

#[fit] ISO8601

---

#[fit] >> 🤔 <<

---

![fit](issues-with-dates.png)

---

![fit](iso-formatter.png)

---

#[fit] Como
#[fit] *descrever*
#[fit] datas

---

#[fit] de maneira
#[fit] *type-safe*
#[fit] e **legível**?

---

#[fit] >> 💡✅ <<

---

#[fit] >> 🎮 <<

---

![fit](playground.png)

---

```swift
protocol DateFormatConvertible {
    var dateFormat: String { get }
}
```

---

```swift
struct DateFormat: DateFormatConvertible {
    let dateFormat: String
}
```

---

```swift
extension DateFormatter {
    func setDateFormat(_ dateFormat: DateFormatConvertible) {
        dateFormat = dateFormat.dateFormat
    }
}
```

---

#[fit] Declarativa

---

```swift
public enum YearStyle: String, DateFormatConvertible {
    case noPadding = "y"
    case twoDigits = "yy"
    case fourDigits = "yyyy"

    public var dateFormat: String { return rawValue }
}
```

---

```swift
public struct DateFormat: DateFormatConvertible {
    public let dateFormat: String

    public init() {
        dateFormat = ""
    }

    internal init(format: DateFormatConvertible) {
        dateFormat = format.dateFormat
    }
}
```

---

#[fit] Conveniência

---

```swift
extension String: DateFormatConvertible {
    public var dateFormat: String { return self }
}

public func + (lhs: DateFormatConvertible, rhs: DateFormatConvertible) -> DateFormatConvertible {
    return lhs.dateFormat + rhs.dateFormat
}
```

---

```swift
internal init(formats: [DateFormatConvertible]) {
    dateFormat = formats.reduce("", +).dateFormat
}
```

---

#[fit] Como deixar
#[fit] __bonito__*?*

---

#[fit] >> 💁🏼 <<

---

```swift
public func year(_ style: YearStyle) -> DateFormat {
    return DateFormat(formats: [dateFormat, style])
}
```

---

```swift
let format = DateForrmat()
    .year(.fourDigits)
    .separator(.dash)
    .month(.zeroPaddedNumber)
    .separator(.dash)
    .day(.zeroPaddedNumber)
    .string("T")
    .hour(.zeroPaddedTwentyFourHour)
    .separator(.colon)
    .minute(.zeroPaddedNumber)
    .separator(.colon)
    .second(.zeroPaddedNumber)
    .timezone(.RFC822)
```

---

```swift
let format = DateForrmat()
    .year(.fourDigits)
    .separator(.dash)
    .month(.zeroPaddedNumber)
    .separator(.dash)
    .day(.zeroPaddedNumber)
    .string("T")
    .hour(.zeroPaddedTwentyFourHour)
    .separator(.colon)
    .minute(.zeroPaddedNumber)
    .separator(.colon)
    .second(.zeroPaddedNumber)
    .timezone(.ISO8601)
```

---

#[fit] >> 🎮✅ <<

---

#[fit] >> 📛 <<

---

#[fit] Caterpillar

---

#[fit] >> 🐛 << 

---

```swift
let format = 🐛()
    .year(.fourDigits)
    .separator(.dash)
    .month(.zeroPaddedNumber)
    .separator(.dash)
    .day(.zeroPaddedNumber)
    .string("T")
    .hour(.zeroPaddedTwentyFourHour)
    .separator(.colon)
    .minute(.zeroPaddedNumber)
    .separator(.colon)
    .second(.zeroPaddedNumber)
    .timezone(.ISO8601)
```

---

![fit](caterpillar.png)

---

#[fit] >> 📛✅ <<

---

#[fit] >> 📦 <<

---

![fit](logo-cocoapods.png)

---

#[fit] `> pod lib create [pod name]` 

--- 

#[fit] **duas** coisas

---

#[fit] >> ✌️ << 

---

#[fit] > `.podspec`
#[fit] > `LICENSE`

---

```ruby
Pod::Spec.new do |s|
 s.name = 'Caterpillar'
 s.version = '1.0.0'
 s.license = { :type => "MIT", :file => "LICENSE" }
 s.summary = '🐛 Caterpillar: Type-safe date formats in Swift, no more yyyy-MM-dd\'T\'HH:mm:ssZ'
 s.homepage = 'https://github.com/fpg1503'
 s.social_media_url = 'https://twitter.com/fpg1503'
 s.authors = { "Francesco Perrotti-Garcia" => "fpg1503@gmail.com" }
 s.source = { :git => "https://github.com/fpg1503/Caterpillar.git", :tag => "v"+s.version.to_s }
 s.platforms     = { :ios => "8.0", :osx => "10.10", :tvos => "9.0", :watchos => "2.0" }
 s.requires_arc = true

 s.default_subspec = "Core"
 s.subspec "Core" do |ss|
     ss.source_files  = "Sources/*.swift"
     ss.framework  = "Foundation"
 end

end
```

---

#[fit] `> pod lib lint`

---

#[fit] `> pod trunk push [NAME].podspec`

---

#[fit] Centralizado

---

#[fit] **des**centralizados

---

![fit](logo-carthage.png)

---

#[fit] Because Carthage has
#[fit] no _centralized list_, and
#[fit] no _project specification format_, 
#[fit] **most frameworks**
#[fit] **should build automatically.**


---

#[fit] `share`
#[fit] _seus_
#[fit] `schemes`

---

#[fit] >> 🎩 <<

---

#[fit] dependências
#[fit] *tem*
#[fit] dependências

---

#[fit] `Cartfile`

---

![fit](logo-swift.png)

---

#[fit] `Package.swift`
^ manifest

---

#[fit] `import PackageDescription`

---

#[fit] By convention, a package includes
#[fit] any source files located in
#[fit] the `Sources/` directory.

---

```
example-package-playingcard
├── Sources
│   ├── PlayingCard.swift
│   ├── Rank.swift
│   └── Suit.swift
└── Package.swift
```

---

```swift
import PackageDescription

let package = Package(
    name: "Caterpillar",
    dependencies: [],
    exclude: ["Tests"]
)
```

---

#[fit] >> 📦✅ <<

---

#[fit] >> 🚀 <<

---

#[fit] `README.md`

---

- Badges
- Requirements
- Usage
- Installation
- Acknowledgments
- License

---

#[fit] Badges

---

![fit](badges.png)

---

#[fit] Requirements

---

```
iOS 8.0+ / Mac OS X 10.10+ / tvOS 9.0+ / watchOS 2.0+
Xcode 8.0+
```

---

#[fit] Usage

---

#[fit] Installation

---

#[fit] Acknowledgments

---

#[fit] License

---

#[fit] Pick a License

---

#[fit] Teste!!

---

#[fit] >> 🔨 <<

---

#[fit] __Crie__
#[fit] um
#[fit] _projeto_

---

#[fit] __Importe__
#[fit] seu
#[fit] _framework_

---

#[fit] Use!

---

#[fit] Visibility

---

#[fit] `open`

---

#[fit] `public`

---

#[fit] `internal`

---

#[fit] `fileprivate`

---

#[fit] `private`

---

#[fit] __Pronto__
#[fit] e
#[fit] _usável_

---

#[fit] 👍👍🏿👍🏻👍🏾👍🏼👍🏽 

---

#[fit] >> 🍒🍰 <<

---

#[fit] Continuous Integration

---

#[fit] `travis-ci`

---

#[fit] `.travis.yml`

---

```
language: objective-c
osx_image: xcode8.2

git:
  submodules: false

env:
  global:
    - LC_CTYPE=en_US.UTF-8
    - LANG=en_US.UTF-8
    - WORKSPACE=Caterpillar.xcworkspace
    - IOS_FRAMEWORK_SCHEME="Caterpillar-iOS"
    - OSX_FRAMEWORK_SCHEME="Caterpillar-macOS"
    - TVOS_FRAMEWORK_SCHEME="Caterpillar-tvOS"
    - WATCHOS_FRAMEWORK_SCHEME="Caterpillar-watchOS"
    - IOS_SDK=iphonesimulator10.2
    - OSX_SDK=macosx10.12
    - TVOS_SDK=appletvsimulator10.1
    - WATCHOS_SDK=watchsimulator3.1
  matrix:
    - DESTINATION="OS=10.2,name=iPhone 7 Plus"              SCHEME="$IOS_FRAMEWORK_SCHEME"     SDK="$IOS_SDK"     RUN_TESTS="NO"  RELEASE_READY="YES" POD_LINT="YES"
    - DESTINATION="OS=9.0,name=iPhone 6s"                   SCHEME="$IOS_FRAMEWORK_SCHEME"     SDK="$IOS_SDK"     RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=8.1,name=iPhone 5"                    SCHEME="$IOS_FRAMEWORK_SCHEME"     SDK="$IOS_SDK"     RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="arch=x86_64"                             SCHEME="$OSX_FRAMEWORK_SCHEME"     SDK="$OSX_SDK"     RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=10.1,name=Apple TV 1080p"             SCHEME="$TVOS_FRAMEWORK_SCHEME"    SDK="$TVOS_SDK"    RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=9.0,name=Apple TV 1080p"              SCHEME="$TVOS_FRAMEWORK_SCHEME"    SDK="$TVOS_SDK"    RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=3.1,name=Apple Watch Series 2 - 42mm" SCHEME="$WATCHOS_FRAMEWORK_SCHEME" SDK="$WATCHOS_SDK" RUN_TESTS="NO"   RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=2.0,name=Apple Watch - 38mm"          SCHEME="$WATCHOS_FRAMEWORK_SCHEME" SDK="$WATCHOS_SDK" RUN_TESTS="NO"   RELEASE_READY="NO"  POD_LINT="NO"

before_install:
  - gem install cocoapods --pre --no-rdoc --no-ri --no-document --quiet
  - brew update
  - brew outdated carthage || brew upgrade carthage

before_script:
  - sh scripts/bootstrap

script:
  - set -o pipefail
  - xcodebuild -version
  - xcodebuild -showsdks

  # Build Framework in Debug and Run Tests if specified
  - if [ $RUN_TESTS == "YES" ]; then
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK" -destination "$DESTINATION" -configuration Debug ONLY_ACTIVE_ARCH=NO ENABLE_TESTABILITY=YES test | xcpretty -c;
    else
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK" -destination "$DESTINATION" -configuration Debug ONLY_ACTIVE_ARCH=NO build | xcpretty -c;
    fi

  # Build Framework in Release and Run Tests if specified
  - if [ $RUN_TESTS == "YES" ]; then
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK" -destination "$DESTINATION" -configuration Release ONLY_ACTIVE_ARCH=NO ENABLE_TESTABILITY=YES test | xcpretty -c;
    else
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK" -destination "$DESTINATION" -configuration Release ONLY_ACTIVE_ARCH=NO build | xcpretty -c;
    fi

  # Run `pod lib lint` if specified
  - if [ $POD_LINT == "YES" ]; then
     pod lib lint;
   fi

before_deploy:
  - carthage build --no-skip-current
  - carthage archive Caterpillar

deploy:
  - provider: releases
    api_key:
      secure:
    file:
      - Caterpillar.framework.zip
    skip_cleanup: true
    overwrite: true
    on:
      repo: fpg1503/Caterpillar
      tags: true
      condition: $RELEASE_READY = YES
  - provider: script
    script: pod trunk push
    on:
      tags: true
      condition: $RELEASE_READY = YES

```

---

```
language: objective-c
osx_image: xcode8.2

git:
  submodules: false
```

---

```
env:
  global:
    - LC_CTYPE=en_US.UTF-8
    - LANG=en_US.UTF-8
    - WORKSPACE=Caterpillar.xcworkspace
    - IOS_FRAMEWORK_SCHEME="Caterpillar-iOS"
    - OSX_FRAMEWORK_SCHEME="Caterpillar-macOS"
    - TVOS_FRAMEWORK_SCHEME="Caterpillar-tvOS"
    - WATCHOS_FRAMEWORK_SCHEME="Caterpillar-watchOS"
    - IOS_SDK=iphonesimulator10.2
    - OSX_SDK=macosx10.12
    - TVOS_SDK=appletvsimulator10.1
    - WATCHOS_SDK=watchsimulator3.1
```

---

```
env:
  matrix:
    - DESTINATION="OS=10.2,name=iPhone 7 Plus"              SCHEME="$IOS_FRAMEWORK_SCHEME"     SDK="$IOS_SDK"     RUN_TESTS="NO"  RELEASE_READY="YES" POD_LINT="YES"
    - DESTINATION="OS=9.0,name=iPhone 6s"                   SCHEME="$IOS_FRAMEWORK_SCHEME"     SDK="$IOS_SDK"     RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=8.1,name=iPhone 5"                    SCHEME="$IOS_FRAMEWORK_SCHEME"     SDK="$IOS_SDK"     RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="arch=x86_64"                             SCHEME="$OSX_FRAMEWORK_SCHEME"     SDK="$OSX_SDK"     RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=10.1,name=Apple TV 1080p"             SCHEME="$TVOS_FRAMEWORK_SCHEME"    SDK="$TVOS_SDK"    RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=9.0,name=Apple TV 1080p"              SCHEME="$TVOS_FRAMEWORK_SCHEME"    SDK="$TVOS_SDK"    RUN_TESTS="NO"  RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=3.1,name=Apple Watch Series 2 - 42mm" SCHEME="$WATCHOS_FRAMEWORK_SCHEME" SDK="$WATCHOS_SDK" RUN_TESTS="NO"   RELEASE_READY="NO"  POD_LINT="NO"
    - DESTINATION="OS=2.0,name=Apple Watch - 38mm"          SCHEME="$WATCHOS_FRAMEWORK_SCHEME" SDK="$WATCHOS_SDK" RUN_TESTS="NO"   RELEASE_READY="NO"  POD_LINT="NO"

```

---

```
before_install:
  - gem install cocoapods --pre --no-rdoc --no-ri --no-document --quiet
  - brew update
  - brew outdated carthage || brew upgrade carthage

before_script:
  - sh scripts/bootstrap

```

---

```
script:
  - set -o pipefail
  - xcodebuild -version
  - xcodebuild -showsdks

  # Build Framework in Debug and Run Tests if specified
  - if [ $RUN_TESTS == "YES" ]; then
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK"
      -destination "$DESTINATION" -configuration Debug ONLY_ACTIVE_ARCH=NO
      ENABLE_TESTABILITY=YES test | xcpretty -c;
    else
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK"
      -destination "$DESTINATION" -configuration Debug ONLY_ACTIVE_ARCH=NO
      build | xcpretty -c;
    fi
```

---


```
script:
  # Build Framework in Release and Run Tests if specified
  - if [ $RUN_TESTS == "YES" ]; then
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK"
      -destination "$DESTINATION" -configuration Release ONLY_ACTIVE_ARCH=NO ENABLE_TESTABILITY=YES
      test | xcpretty -c;
    else
      xcodebuild -workspace "$WORKSPACE" -scheme "$SCHEME" -sdk "$SDK"
      -destination "$DESTINATION" -configuration Release ONLY_ACTIVE_ARCH=NO
      build | xcpretty -c;
    fi

  # Run `pod lib lint` if specified
  - if [ $POD_LINT == "YES" ]; then
     pod lib lint;
   fi
```

---

#[fit] Deploy Carthage

---

#[fit] Testes

---

#[fit] Teste!

---

#[fit] >> 🛠🛠🛠 << 

---

#[fit] `public`
#[fit] **deve** ser testada

---

#[fit] Cobertura de teste
#[fit] **deve** ser 100%

---

#[fit] What is
#[fit] **code coverage**?

---

#[fit] Code Coverage

^ In computer science, code coverage is a measure used to describe the degree to which the source code of a program is executed when a particular test suite runs.

---

#[fit] 👍 `fpg1503/GoodCodeTalk`

---

#[fit] Docs

---

#[fit] >> 📖 <<

---

#[fit] >> 🚀✅ <<

---

#[fit] Que **chato**
#[fit] fazer isso sempre

---

#[fit] >> 🍪✂️ <<

---

#[fit] `cookiecutter-swift/FrameworkTemplate`

---

#[fit] 📱📺⌚️🖥

---

#[fit] travis

---

#[fit] cocoapods

---

#[fit] Carthage

---

#[fit] SwiftPM

---

#[fit] playground

---

#[fit] README

---

#[fit] `github.com/fpg1503/MakingFrameworksTalk`

---

#[fit] `github.com/fpg1503/Talks`

---

#[fit] Obrigado!

---

#[fit] >> 🐥 <<

---

#[fit] @fpg1503