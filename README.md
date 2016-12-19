# Immutable Undo

Simple data structure for and undo/redo stack, using ImmutableJS. The structure holds a stack of undo states, and a stack of redo states. It does not keep a reference to the current state to avoid duplicating data if your state is already stored in another structure.

## Installation

``` bash
npm install --save immutable-undo
```

## Reference

### Static

#### `History.create`

- `{Object} [opts]` Option object
- `{Number} [opts.maxUndos=500]` Maximum number of undos stored. Beyond that, the oldest undo is dropped.
- `return {History}` An empty history

``` js
var history = History.create({
    maxUndos: 100
});
```

### Properties

#### `canUndo`

- `return {Boolean}` True if the history has undos

#### `canRedo`

- `return {Boolean}` True if the history has redos

#### `previous`

- `return {State | Undefined}` The most recent state in the undo stack

#### `next`

- `return {State | Undefined}` The most recent state in the redo stack

### Methods

#### `push`

- `{State} newState` The state to push on top of the undo stack
- `return {History}`

Pushes a new state on the undo stack, and clears the redo stack

#### `undo`

- `{State} current` The current state, that will be pushed on the redo stack
- `return {History}` The history with the undo stack popped once, and the current state added to redos.

#### `redo`

- `{State} current` The current state, that will be pushed on the undo stack
- `return {History}` The history with the redo stack popped once, and the current state added to redos