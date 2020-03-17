# @aphorica/vuetify-icon-stack

github: https://aphorica.github.com<br/>
Web: https://aphorica.com

## Installing

`npm install @aphorica/vuetify-icon-stack`

or

`yarn add @aphorica/vuetify-icon-stack`

## Running the Demo

In a command prompt, cd info the 'demo' directory, and:

```
  (yarn|npm) install
  (yarn|npm run) serve)
```

Open a browser on `localhost:8080`

Click the buttons in the toolbar to reset the iconStack
component state (in the center of the page).

Click on the iconStack component for it to emit its
current state.

## Overview

Extremely light implementation of an icon stack.

Each icon is associated with a state.  When a state is
subsequently set, the associated icon becomes visible and
clickable.

Stack order does not change, only button visibility changes.

Clicking on the icon stack emits the associated state with
the visible icon.

You simply provide your own v-icons in the slot.  This
allows for the most flexibility in usage and defining
your icon sets.

Note the `data-state` attribute required for each icon
in the __Usage__ section below.

## Usage

The module is impemented as a simple container with a 
single slot for your icons.  Icons must be tagged with
a `data-state` attribute specifying the state for that
icon.  State can be anything.

Example (from the attached demo):

```
        <vuetify-icon-stack :initialState="currentState"
          @clicked="onStackIconClicked">
          <v-icon data-state="add" color="primary" x-large>mdi-plus-circle</v-icon>
          <v-icon data-state="commit" color="primary" x-large>mdi-check-circle</v-icon>
          <v-icon data-state="abort" color="black" x-large>mdi-close-circle</v-icon>
        </vuetify-icon-stack>
```

The stack's current state is set by using EventBus to
emit a message to it:

```
      EventBus.$emit('set-vuetify-icon-stack-state', state)
```

Note that if you send an invalid state, it will silently fail.

The component requires a single prop, `initialState`, which
is required.

```
        <vuetify-icon-stack :initialState="currentState">
          ...
          ...
        </vuetify-icon-stack>
```

