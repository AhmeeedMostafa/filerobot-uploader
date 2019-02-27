# Filerobot Uploader

The Filerobot Uploader is a multi-function Uploader that will make uploads super easy in your web sites and apps. It is fast to integrate allows end users to upload media, files and any assets via Filerobot's reverse CDN. Files are stored into scalable and flexible Cloud storage, optimised and delivered over CDN to your end users rocekt fast. Features include inline image editing, auto-tagging, auto-cropping and many more.

![Filerobot Uploader View](https://scaleflex.airstore.io/filerobot/assets/filerobot-uploader.png)


[See demo](https://scaleflex.github.io/filerobot-uploader/)

## Table of contents

* [Standalone usage](#standalone_usage)
    * [Installation](#installation)
    * [Quick start](#quick_start)
    * [Methods](#methods)
* [React component usage](#react_component)
    * [Installation](#installation_react)
    * [Quick start](#quick_start_react)
    * [Methods/Properties](#methods_react)
* [Configuration](#configuration)
* [Full features config example](#full_example)
* [Contributing](#contributing)

## <a name="standalone_usage"></a>Standalone usage

### <a name="installation"></a>Installation

Use latest CDNized plugin version

```
<script src="https://scaleflex.airstore.io/filerobot/uploader/1.2.1/main.min.js"></script>
```

### <a name="quick_start"></a>Quick start

We provide easy way to integrate image uploader in your applications

```
<script>
  let config = {
    container: 'example',
    filerobotUploadKey: '0cbe9ccc4f164bf8be26bd801d53b132',
    openpixKey: 'xxxxxxxxxxxxxxx'
  };
  let onUpload = (files) => {
     console.log('files: ', files);
     alert('Files uploaded successfully! check the console to see the uploaded files');
  };
  let uploader = FilerobotUploader.init(config, onUpload);

  uploader.open();
</script>
```

### <a name="methods"></a>Methods

#### `window.FilerobotUploader.init(config: {}, uploadHandler: callback)`: function

Initialization of Filerobot Uploader plugin.

#### `window.FilerobotUploader.open(tab : string, options: {})`: function

Open uploader modal.

* **tab**: string (optional, default: 'UPLOAD') - allow to choose the initial tab (should be one of enabled modules)

* **options**: {} (optional) - options for tabs

#### `window.FilerobotUploader.close()`: function

Close uploader modal.

#### `window.FilerobotUploader.unmount()`: function

Destroy uploader

## <a name="react_component"></a>React component usage

### <a name="installation_react"></a>Installation

```
$ npm install --save filerobot-uploader
```

### <a name="quick_start_react"></a>Quick start

We provide easy way to integrate image uploader in your applications

```
import React, { Component } from 'react';
import { render } from 'react-dom';
import FilerobotUploader from 'filerobot-uploader';


const config = {
  modules: ['UPLOAD', 'MY_GALLERY', 'ICONS_GALLERY', 'IMAGES_GALLERY', 'TAGGING', 'IMAGE_EDITOR'],
  uploadParams: { dir:"/demo_filerobot_en" },
  filerobotUploadKey: '7cc1f659309c480cbc8a608dc6ba5f03',
  container: 'scaleflex-tests-v5a'
}

class App extends Component {
  constructor() {
    super();

    this.state = {
      isShow: false
    }
  }

  render() {
    return (
      <div>
        <h1>React Example</h1>
        <button onClick={() => { this.setState({ isShow: true }); }}>Click</button>
        <FilerobotUploader
          opened={this.state.isShow}
          config={config}
          onClose={() => { this.setState({ isShow: false }); }}
          onUpload={(img) => { console.log(img) }}
        />
      </div>
    )
  }
}

render(<App/>, document.getElementById('app'));
```

### <a name="methods_react"></a>Methods/Properties

#### `opened`: bool (required)

**default**: false

Trigger to display the uploader widget.

#### `initialTab`: string (optional)

**default**: 'UPLOAD'

Allow to choose the initial tab. Should be one of enabled modules.

#### `config`: object (required)

Uploader config.

#### `onClose()`: function (required)

Close uploader widget.

#### `onUpload(files: file[])`: function (required)

Function to handle uploaded files.

## <a name="configuration"></a>Configuration

#### `container`: string (required)

Filerobot Container name.

```
let config = {
    ...,

    container: 'example'
};
```

#### `filerobotUploadKey`: string (required)

Unique upload key for Filerobot.

```
let config = {
    ...,

    filerobotUploadKey: 'xxxxxxxxxxxx'
};
```

#### `openpixKey`: string (required)

Key for Openpix. Required if you are using "ICONS_GALLERY", "IMAGES_GALLERY"

```
let config = {
    ...,

    openpixKey: 'xxxxxxxxxxxx'
};
```

#### `language`: string

**default**: 'en'

Language of uploader

available languages: en, fr, de, ru

```
let config = {
    ...,

    language: 'en'
};
```

#### `modules`: string[]

**default**: ["UPLOAD", "MY_GALLERY", "ICONS_GALLERY", "IMAGES_GALLERY"]

Modules (tabs) in file uploader modal.

**Available modules**: **UPLOAD**, **MY_GALLERY**, **ICONS_GALLERY**, **IMAGES_GALLERY**, **TAGGING**, **IMAGE_EDITOR**

```
let config = {
    ...,

    modules: ['UPLOAD', 'ICONS_GALLERY', 'TAGGING']
};
```

#### `uploadParams`: object

[see documentation](https://docs.airstore.io/go/airstore-public-documentation/en/airstore-api-reference/upload-files/#od_9911d3cb)

* **dir**: string (default: '/') - specify the folder where you want to upload the file. If the folder doesn't exist, it will be created.

```
let config = {
    ...,

    uploadParams: {
        dir: '/folder_name',
        ...
    }
};
```

#### `initialTab`: string

**default**: 'UPLOAD'

Allow to choose the initial tab. Should be one of enabled modules.

```
let config = {
    ...,

    initialTab: 'UPLOAD'
};
```

#### `folderBrowser`: bool

**default**: true

Aside menu to browse folders in your container.

```
let config = {
    ...,

    folderBrowser: true
};
```

#### `tagging`: object

* `key`: string (require) - key to use image recognition technology

* `autoTaggingButton`: bool - adds button which will automatically generate tags based on image recognition technology

* `provider`: string [google|imagga] - recognition provider

* `confidence`: number [0..100] - confidence of recognition

* `limit`: number - limit of tags generated by image recognition technology

```
let config = {
    ...,

    tagging: {
        autoTaggingButton: true,
        provider: 'google',
        confidence: 60,
        limit: 10,
        key: 'xxxxx'
    }
};
```

#### `colorScheme`: object

* `active` string (default: 'default')- active theme scheme

* `custom`: object - custom color scheme

* `custom.mainBackground`: color - main background

* `custom.navBackground`: color - nav background

* `custom.buttonBackground`: color - button background

* `custom.hoverButtonBackground`: color - button background on hover

* `custom.inputBackground`: color - search field background

* `custom.inputOutlineColor`: color - search field outline

* `custom.activeTabBackground`: color - current nav tab background

* `custom.text`: color - text

* `custom.title`: color - title

* `custom.inputTextColor`: color - search field text

* `custom.tabTextColor`: color - nav tab text

* `custom.activeTabTextColor`: color - current nav tab text

* `custom.buttonTextColor`: color - button text

* `custom.border`: color - draggable boundaries border


```
let config = {
    ...,

    colorScheme: {
       active: 'custom',

       custom: {
         mainBackground: '#f5f5f5',
         navBackground: '#181830',
         buttonBackground: '#00707C',
         hoverButtonBackground: '#096868',
         inputBackground: '#fff',
         inputOutlineColor: '#4d90fe',
         activeTabBackground: '#40545b',
         text: '#5d636b',
         title: '#1e262c',
         inputTextColor: '#555555',
         tabTextColor: '#c0c1c1',
         activeTabTextColor: '#fff',
         buttonTextColor: '#fff',
         border: '#d8d8d8'
       }
    }
};
```

## <a name="full_example"></a>Full features config example

```
<script>
  let config = {
    modules: ['UPLOAD', 'MY_GALLERY', 'ICONS_GALLERY', 'IMAGES_GALLERY', 'TAGGING', 'IMAGE_EDITOR'],
    uploadParams: {
      dir: '/your_root_folder'
    },
    filerobotUploadKey: '0cbe9ccc4f164bf8be26bd801d53b132',
    container: 'example',
    openpixKey: 'xxxxxxxxxxxxxxx',
    initialTab: 'UPLOAD',
    folderBrowser: true,
    tagging: {
      executeAfterUpload: true,
      autoTaggingButton: true,
      provider: 'google',
      confidence: 60,
      limit: 10,
      key: 'aaaa'
    },
    language: 'en',

    colorScheme: {
      active: 'custom',
      custom: {
        mainBackground: '#f5f5f5',
        navBackground: '#181830',
        buttonBackground: '#00707C',
        hoverButtonBackground: '#096868',
        inputBackground: '#fff',
        inputOutlineColor: '#4d90fe',
        activeTabBackground: '#40545b',
        text: '#5d636b',
        title: '#1e262c',
        inputTextColor: '#555555',
        tabTextColor: '#c0c1c1',
        activeTabTextColor: '#fff',
        buttonTextColor: '#fff',
        border: '#d8d8d8'
      }
    }
  };
  let onUpload = (files) => {
    console.log('files: ', files);
    alert('Files uploaded successfully! check the console to see the uploaded files');
  };
  let uploader = FilerobotUploader.init(config, onUpload);
  let button = document.createElement('button');

  button.onclick = () => { uploader.open(); }
  button.innerText = 'Open Uploader';
  document.body.appendChild(button);
</script>
```

## <a name="contributing"></a>Contributing!

All contributions are super welcome!