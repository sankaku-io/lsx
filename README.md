### [lsx - React plugin for LiveScript](https://github.com/sakanabiscuit/lsx)

! This plugin is written LiveScript, you need to install LiveScript. LiveScript is a language which compiles to JavaScript.

JSX(facebook) need compiler, but LiveScript is not usable together with JSX. This plugin make understandable and simple. This is sample.

    require! \react-dom : ReactDOM
    require! lsx : { Live, init, div, a, p }

    Main = init class extends Live
        render: ->
            div [],
                p [] \hello
                a [] \world

    window.onload = ->
        \app |> document.createElement
             |> document.body.appendChild
        ReactDOM.render do
            Main []
            \app |> document.querySelector

### Installation

Have Node.js installed.

    npm i -D lsx

### Usage

1 import plugin "lsx".

    require! lsx : { Live, init, div, a, p }

2 create class and bind. (example:Main)

    Main = init class extends Live

        render: ->
            div [],
                p [] \hello
                a [] \world

3 render.

    ReactDOM.render do
        Main []
        \app |> document.querySelector

### Function

component

    div [] \hello,world

    # <div>hello,world</div>

null contents component

    div []

    # <div />

nest component

    div [],
        p []
        p [] \hello,world

    # <div>
    #     <p />
    #     <p>hello,world</p>
    # </div>

set props and style, etc..

    div [ test-prop:\test
        , onClick: @test-func
        , style:
          height: 200
          width:  200 ] \hello,world

    # <div test-prop = "test"
    #      onClick = {this.testFunc}
    #      style = {
    #          height:200
    #          width:200
    #      }>
    #     hello,world
    # <div>

use component and set prop-types

    require! lsx : { Live, init, type, div }

    test-component = init class extends Live

        @prop-types =
            test-class:type.string

        @default-props =
            test-class:\default

        render: ->
            div [ class-name: @props.test-class ] @props.children

    Main = init class extends Live

        render: ->
            div [],
                test-component [ test-class: \test ] \hello,world

use plain component

    Test-component = React.createClass
        render: ->
            React.DOM.div null, 'hello,world'

    test-component = init Test-component

    ReactDOM.render do
        test-component []
        \app |> document.querySelector
