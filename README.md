# scratch-blocks
#### Scratch Blocks is a library for building creative computing interfaces.
[![Build Status](https://travis-ci.org/LLK/scratch-blocks.svg?branch=develop)](https://travis-ci.org/LLK/scratch-blocks)
[![Dependency Status](https://david-dm.org/LLK/scratch-blocks.svg)](https://david-dm.org/LLK/scratch-blocks)
[![devDependency Status](https://david-dm.org/LLK/scratch-blocks/dev-status.svg)](https://david-dm.org/LLK/scratch-blocks#info=devDependencies)

![](https://cloud.githubusercontent.com/assets/747641/15227351/c37c09da-1854-11e6-8dc7-9a298f2b1f01.jpg)

## Introduction
Scratch Blocks is a fork of Google's [Blockly](https://github.com/google/blockly) project that provides a design specification and codebase for building creative computing interfaces. Together with the [Scratch Virtual Machine (VM)](https://github.com/LLK/scratch-vm) this codebase allows for the rapid design and development of visual programming interfaces. Unlike [Blockly](https://github.com/google/blockly), Scratch Blocks does not use [code generators](https://developers.google.com/blockly/guides/configure/web/code-generators), but rather leverages the [Scratch Virtual Machine](https://github.com/LLK/scratch-vm) to create highly dynamic, interactive programming environments.

*This project is in active development and should be considered a "developer preview" at this time.*

## Two Types of Blocks
![](https://cloud.githubusercontent.com/assets/747641/15255731/dad4d028-190b-11e6-9c16-8df7445adc96.png)

Scratch Blocks brings together two different programming "grammars" that the Scratch Team has designed and continued to refine over the past decade. The standard [Scratch](https://scratch.mit.edu) grammar uses blocks that snap together vertically, much like LEGO bricks. For our [ScratchJr](https://scratchjr.org) software, intended for younger children, we developed blocks that are labelled with icons rather than words, and snap together horizontally rather than vertically. We have found that the horizontal grammar is not only friendlier for beginning programmers but also better suited for devices with small screens.

## Documentation
The "getting started" guide including [FAQ](https://scratch.mit.edu/developers#faq) and [design documentation](https://github.com/LLK/scratch-blocks/wiki/Design) can be found in the [wiki](https://github.com/LLK/scratch-blocks/wiki).

## Donate
We provide [Scratch](https://scratch.mit.edu) free of charge, and want to keep it that way! Please consider making a [donation](https://secure.donationpay.org/scratchfoundation/) to support our continued engineering, design, community, and resource development efforts. Donations of any size are appreciated. Thank you!

#2020-08-30 Critcal issue clear 
컴파일 시 이런 문제가 발생한다. 이 문제는 추후 gui와 link를 걸어 컴파일 하는데 에러가 나는 요소 이기 때문에 반드시 고쳐 주어야 한다.
```
    ERROR in ./shim/blockly_compressed_horizontal.js
    Module not found: Error: Can't resolve '../blockly_compressed_horizontal' in 'C:\Users\kch\Desktop\Develope\Arduino\scratch-blocks\shim'
     @ ./shim/blockly_compressed_horizontal.js 1:17-116
     @ ./shim/blockly_compressed_horizontal.goog.js
     @ ./node_modules/imports-loader?Blockly=../shim/blocks_compressed_horizontal-blockly_compressed_horizontal-messages,goog=../shim/blockly_compressed_horizontal.goog!./node_modules/exports-loader?Blockly!./msg/scratch_msgs.js
     @ ./shim/horizontal.js
```
```
    ERROR in ./shim/blockly_compressed_vertical.js
    Module not found: Error: Can't resolve '../blockly_compressed_vertical' in 'C:\Users\kch\Desktop\Develope\Arduino\scratch-blocks\shim'
     @ ./shim/blockly_compressed_vertical.js 1:17-114
     @ ./shim/blockly_compressed_vertical.goog.js
     @ ./node_modules/imports-loader?Blockly=../shim/blocks_compressed_vertical-blockly_compressed_vertical-messages,goog=../shim/blockly_compressed_vertical.goog!./node_modules/exports-loader?Blockly!./msg/scratch_msgs.js
     @ ./shim/vertical.js
```
이 문제는 간단하게 경로만 바꾸어 주면 쉽게 해결 가능하다. 
.shim/blockly_compressed_horizontal.js 파일에서 
```
module.exports = require('imports-loader?this=>window!exports-loader?Blockly&goog!../blockly_compressed_horizontal');
```
이 문장을 아래와 같이 바꿔준다. 물론 다른 경로(vertical)도 마찬가지로 아래와 같이 변경해주면 더 이상 에러는 나오지 않게 된다.  
```
module.exports = require('imports-loader?this=>window!exports-loader?Blockly&goog!./blockly_compressed_horizontal');
```
