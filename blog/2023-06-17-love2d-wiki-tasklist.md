# 2023年6月17日 - LÖVE modules

作業対象の更新と調査用に使う記事です(未完成)。2023年6月17日現在の情報であり未完成です。

version.12.0 以降については別の機会とします。

## love

### Functions

* ✅love.getVersion
* ✅love.hasDeprecationOutput
* ✅love.isVersionCompatible
* ✅love.setDeprecationOutput

### Callbacks　
#### General 更新完了 (最終確認日: 2023年7月8日)

* ✅[Config Files](https://love2d.org/wiki/Config_Files)
* ✅love.draw
* ✅love.errhand
* ✅love.errorhandler
* ✅love.load
* ✅love.lowmemory
* ✅love.quit
* ✅love.run
* ✅love.threaderror
* ✅[love.update](https://love2d.org/wiki/)

#### Window 更新完了 (最終確認日: 2023年7月8日)

* ✅love.directorydropped
* ✅love.displayrotatededed
* ✅love.filedropped
* ✅love.focus
* ✅love.mousefocus
* ✅love.resize
* ✅love.visible

#### Keyboard 更新完了 (最終確認日: 2023年7月8日)

* ✅love.keypressed
* ✅love.keyreleased
* ✅love.textedited
* ✅love.textinput

#### Mouse 更新完了 (最終確認日: 2023年7月8日)

* ✅[love.mousemoved](https://love2d.org/wiki/love.mousemoved)
* ✅[love.mousepressed](https://love2d.org/wiki/love.mousepressed)
* ✅[love.mousereleased](https://love2d.org/wiki/love.mousereleased)
* ✅love.wheelmoved

#### Joystick 更新完了 (最終確認日: 2023年7月10日)

* ✅love.gamepadaxis
* ✅love.gamepadpressed
* ✅love.gamepadreleased
* ✅love.joystickadded
* ✅love.joystickaxis
* ✅love.joystickhat
* ✅love.joystickpressed
* ✅love.joystickreleased
* ✅love.joystickremoved

#### Touch 更新完了 (最終確認日: 2023年7月8日)

* ✅love.touchmoved
* ✅love.touchpressed
* ✅love.touchreleased

## love.audio

* love.audio.newQueueableSource
* love.audio.newSource
* love.audio.play
* love.audio.setEffect
* EffectType
* Source
* Source:getFreeBufferCount
* ✅Source:isPaused
* Source:queue
* Source:setEffect
* Source:setFilter
* Source:setRelative

## love.data

* Data:getFFIPointer
* ✅Data:getString
* ✅love.data.newDataView

## love.event

* ✅love.event.pump
* ✅love.event.push
* love.event.quit
* love.event.wait

## love.filesystem

* ✅love.filesystem
* ✅(File):seek
* ✅love.filesystem.getDirectoryItems
* ✅love.filesystem.getIdentity
* love.filesystem.lines
* love.filesystem.load
* ✅love.filesystem.mount
* love.filesystem.newFileData
* ✅love.filesystem.read
* ✅love.filesystem.remove
* ✅love.filesystem.setIdentity
* ✅love.filesystem.write

## love.font

* love.font
* love.font.newBMFontRasterizer
* love.font.newImageRasterizer
* love.font.newRasterizer
* love.font.newTrueTypeRasterizer
* PixelFormat

## love.graphics
* ✅love.graphics

## Types
* Canvas
* Canvas:clear
* ✅Canvas:generateMipmaps
* ✅Canvas:getFSAA
* ✅Canvas:getFormat
* ✅Canvas:getImageData
* ✅Canvas:getMSAA
* ✅Canvas:getMipmapMode
* ✅Canvas:getPixel
* ✅Canvas:newImageData
* Canvas:renderTo
* ✅Drawable
* ✅Font
* ✅Font:getAscent
* ✅Font:getBaseline
* ✅Font:getDPIScale
* ✅Font:getDescent
* ✅Font:getFilter
* ✅Font:getHeight
* Font:getKerning
* ✅Font:getLineHeight
* ✅Font:getWidth
* Font:getWrap
* ✅Font:hasGlyphs
* ✅Font:setFallbacks
* ✅Font:setFilter
* ✅Font:setLineHeight
* ✅Framebuffer
* ✅Framebuffer:getImageData
* ✅Framebuffer:getWrap
* ✅Framebuffer:renderTo
* ✅Framebuffer:setWrap
* Image
* (Image):getData
* (Image):getFlags
* ✅(Image):isCompressed
* (Image):isFormatLinear
* ✅(Image):refresh
* ✅(Image):replacePixels
* Mesh
* Mesh:attachAttribute
* Mesh:setTexture
* Mesh:setVertexMap
* Mesh:setVertices
* Mesh:setVertexAttribute
* VertexAttributeStep
* ✅ParticleSystem
* ✅ParticleSystem:clone
* ✅ParticleSystem:count 
* ✅ParticleSystem:emit
* ✅ParticleSystem:getAreaSpread
* ✅ParticleSystem:getBufferSize
* ParticleSystem:getColors
* ✅ParticleSystem:getCount
* ✅ParticleSystem:getDirection
* ✅ParticleSystem:getEmissionArea
* ✅ParticleSystem:getEmissionRate
* ✅ParticleSystem:getEmitterLifetime
* ✅ParticleSystem:getImage
* ✅ParticleSystem:getInsertMode
* ✅ParticleSystem:getLinearAcceleration
* 
* ParticleSystem:setColors
* ParticleSystem:setQuads
* ParticleSystem:setRotation
* 

### Texture
* ✅Texture
* ✅Texture:getDPIScale
* ✅Texture:getDepth
* ✅Texture:getDepthSampleMode
* ✅Texture:getDimensions
* ✅Texture:getFilter
* ✅Texture:getFormat
* ✅Texture:getHeight
* ✅Texture:getLayerCount
* ✅Texture:getMipmapCount
* ✅Texture:getMipmapFilter
* 
* ✅Texture:isReadable
* Texture:setFilter
* ✅Texture:setMipmapFilter
* ✅Texture:setWrap

## Functions

### Drawing
* ✅love.graphics.arc
* ✅love.graphics.circle
* ✅love.graphics.clear
* ✅love.graphics.discard
* love.graphics.draw
* ✅love.graphics.drawLayer
* ✅love.graphics.drawq
* ✅love.graphics.ellipse
* ✅love.graphics.flushBatch
* love.graphics.line
* ✅love.graphics.point
* ✅love.graphics.points
* love.graphics.polygon
* ✅love.graphics.present
* love.graphics.print
* ✅love.graphics.printf
* ✅love.graphics.quad
* love.graphics.rectangle
* ✅love.graphics.stencil
* ✅love.graphics.triangle

### Object Creation
* ✅love.graphics.captureScreenshot
* ✅love.graphics.newArrayImage
* love.graphics.newCanvas
* love.graphics.newCubeImage
* love.graphics.newFont
* ✅love.graphics.newFramebuffer
* love.graphics.newImage
* love.graphics.newImageFont
* love.graphics.newMesh
* ✅love.graphics.newParticleSystem
* love.graphics.newPixelEffect
* love.graphics.newQuad
* love.graphics.newScreenshot
* love.graphics.newShader
* love.graphics.newSpriteBatch
* 


## love.image

* ✅CompressedImageData
* ✅CompressedImageData:getDimensions
* ✅CompressedImageData:getFormat
* ✅CompressedImageData:getHeight
* ✅CompressedImageData:getMipmapCount
* ✅CompressedImageData:getWidth
* ImageData
* ImageData:encode
* ✅ImageData:getDimensions
* ✅ImageData:getFormat
* ✅ImageData:getHeight
* ✅ImageData:getPixel
* ✅ImageData:getString
* ✅ImageData:getWidth
* ImageData:mapPixel
* ImageData:paste
* ✅ImageData:setPixel
* ✅love.image
* ✅love.image.isCompressed
* ✅love.image.newCompressedData
* ✅love.image.newEncodedImageData
* CompressedImageFormat
* ImageEncodeFormat
* PixelFormat
* Image Formats

## love.joystick

* ✅love.joystick
* ✅Joystick
* ✅love.joystick.getJoysticks
* ✅Joystick:getAxes
* ✅Joystick:getAxis
* ✅Joystick:getAxisCount
* ✅Joystick:getButtonCount
* ✅Joystick:getDeviceInfo
* ✅Joystick:getGUID
* ✅Joystick:getGamepadAxis
* ✅Joystick:getGamepadMapping
* ✅Joystick:getGamepadMappingString
* ✅Joystick:getGamepadType (12.0)
* ✅Joystick:getHat
* ✅Joystick:getHatCount
* ✅Joystick:getID
* Joystick:getJoystickType (12.0)
* ✅Joystick:getName
* Joystick:getPlayerIndex (12.0)
* ✅Joystick:getVibration
* ✅Joystick:isConnected
* ✅Joystick:isDown
* Joystick:isGamepad
* ✅Joystick:isGamepadDown
* ✅Joystick:isVibrationSupported
* Joystick:setPlayerIndex (12.0)
* ✅Joystick:setVibration
* ✅love.joystick.close
* ✅love.joystick.getAxes
* ✅love.joystick.getAxis
* ✅love.joystick.getBall
* ✅love.joystick.getGamepadMappingString
* ✅love.joystick.getHat
* ✅love.joystick.getJoystickCount
* ✅love.joystick.getJoysticks
* ✅love.joystick.getName
* ✅love.joystick.getNumAxes
* ✅love.joystick.getNumBalls
* ✅love.joystick.getNumButtons
* ✅love.joystick.getNumHats
* ✅love.joystick.getNumJoysticks
* ✅love.joystick.isDown
* ✅love.joystick.isOpen
* ✅love.joystick.loadGamepadMappings
* ✅love.joystick.open
* ✅love.joystick.saveGamepadMappings
* ✅love.joystick.setGamepadMapping
* ✅GamepadAxis
* ✅GamepadButton
* ✅GamepadType (12.0)
* ✅JoystickHat
* ✅JoystickInputType
* ✅JoystickType (12.0)


## love.keyboard - 更新完了 (最終確認日: 2023年6月24日)

* ✅[love.keyboard.isDown](https://love2d.org/wiki/love.keyboard.isDown) - 2023年6月16日 (金) 12:13 
* ✅[love.keyboard.isScancodeDown](https://love2d.org/wiki/love.keyboard.isScancodeDown) - 2023年6月24日 (土) 09:56
* ✅[KeyConstant](https://love2d.org/wiki/KeyConstant) - 2023年6月16日 (金) 11:59
* ✅[Scancode](https://love2d.org/wiki/Scancode) - 2023年6月16日 (金) 12:03

## love.math

* BezierCurve
* love.math.newBezierCurve
* BezierCurve:evaluate
* BezierCurve:getControlPoint
* BezierCurve:getDerivative
* BezierCurve:render
* BezierCurve:renderSegment
* love.math.newRandomGenerator
* RandomGenerator:randomNormal
* RandomGenerator:random
* RandomGenerator
* love.math.newTransform
* love.math.newBezierCurve
* love.math.randomNormal

## love.mouse 更新完了 (最終確認日: 2023年6月27日)

* ✅love.mouse.getCursor - 2023年2月24日 (金) 02:07 
* ✅love.mouse.isCursorSupported - 2023年6月16日 (金) 12:29
* ✅love.mouse.isDown - 2023年6月27日 (火) 15:29
* ✅love.mouse.newCursor - 2023年6月16日 (金) 12:36

## love.physics

## love.sound (最終確認日: 2023年7月23日)

* ✅SoundData:setSample
* ✅love.sound.newDecoder
* ✅love.sound.newSoundData

## love.system 更新完了 (最終確認日: 2023年6月27日)

* ✅love.system - 2023年6月27日 (火) 15:42
* love.system.getPreferredLocales (TBA - v12.0 で実装予定)

## love.thread

* love.thread
* ✅Channel:demand
* ✅Channel:supply

## love.timer

* love.timer.getFPS
* love.timer.getTime
* ✅love.timer.sleep

## love.touch (最終確認日: 2023年6月23日)

* ありません。

## love.video (最終確認日: 2023年7月24日)


* ✅[VideoStream:getFilename](https://love2d.org/wiki/VideoStream:getFilename)
* ✅[VideoStream:isPlaying](https://love2d.org/wiki/VideoStream:isPlaying)
* ✅[VideoStream:pause](https://love2d.org/wiki/VideoStream:pause)
* ✅[VideoStream:play](https://love2d.org/wiki/VideoStream:play)
* ✅[VideoStream:rewind](https://love2d.org/wiki/VideoStream:rewind)
* ✅[VideoStream:seek](https://love2d.org/wiki/VideoStream:seek)
* ✅[VideoStream:setSync](https://love2d.org/wiki/VideoStream:setSync)
* ✅[VideoStream:tell](https://love2d.org/wiki/VideoStream:tell)

## love.window

* [love.window.getDPIScale](https://love2d.org/wiki/love.window.getDPIScale)
* [love.window.getDesktopDimensions](https://love2d.org/wiki/love.window.getDesktopDimensions)
* ✅[love.window.getMode](https://love2d.org/wiki/love.window.getMode)
* ✅[love.window.getPosition](https://love2d.org/wiki/love.window.getPosition)
* ✅[love.window.getSafeArea](https://love2d.org/wiki/love.window.getSafeArea) - 2023年6月17日 (土) 15時11分
* ✅[love.window.setPosition](https://love2d.org/wiki/love.window.setPosition)
* [love.window.setVSync](https://love2d.org/wiki/love.window.setVSync)
* [love.window.updateMode](https://love2d.org/wiki/love.window.updateMode)

## lua-enet

* lua-enet
* host:broadcast
* enet.peer:send
* enet.event

## luasocket

## utf8 更新完了 (最終確認日: 2023年6月27日)

* ✅utf8 - 2023年6月16日 (金) 12:47

## その他

* 0.5.0
* 11.4
* 12.0
* arcLine
* Code Style
* Game Distribution
