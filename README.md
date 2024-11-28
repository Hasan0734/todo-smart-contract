# TodoList Smart Contract

A Solidity-based smart contract for managing a decentralized Todo list. This contract allows users to create, update, toggle completion status, and delete their personal todos. Each todo is uniquely identified and linked to its owner.

## Features

- **Create Todo**: Add a new todo with a unique ID.
- **Update Todo**: Modify the text of an existing todo.
- **Get Todos**: Retrieve all todos belonging to the caller.
- **Toggle Completion**: Mark a todo as completed or incomplete.
- **Delete Todo**: Remove a todo from the list.

---

## Contract Overview

### Struct: `Todo`

A `Todo` represents a task with the following attributes:

- `id` (`uint256`): Unique identifier for the todo.
- `owner` (`address`): Address of the user who owns the todo.
- `text` (`string`): Description of the task.
- `completed` (`bool`): Status of the task (completed or not).
- `timestamp` (`uint256`): Creation timestamp.
- `updated` (`uint256`): Last updated timestamp.

### Events

- `CreteEvent(uint256 id, address indexed owner, string indexed text, uint256 indexed timestamp)`: Triggered when a new todo is created.
- `UpdateEvent(uint256 id, address indexed owner, string indexed text, uint256 indexed updated)`: Triggered when a todo is updated.
- `RemoveEvent(uint256 indexed id, address indexed owner, uint256 indexed timestamp)`: Triggered when a todo is removed.

### State Variables

- `todos`: Dynamic array storing all `Todo` structs.
- `nextId`: Counter for generating unique IDs.

---

## Functions

### `createTodo(string memory _text)`

Creates a new todo.

- **Inputs**: `_text` (Description of the todo)
- **Access**: Public
- **Emits**: `CreteEvent`

---

### `updateTodo(uint256 _id, string memory _text)`

Updates the text of an existing todo.

- **Inputs**: `_id` (Todo ID), `_text` (New description)
- **Access**: Public (Restricted to the owner)
- **Emits**: `UpdateEvent`

---

### `getTodos() public view returns (Todo[] memory)`

Returns all todos belonging to the caller.

- **Outputs**: Array of `Todo` structs.

---

### `toggleComplete(uint256 _id)`

Toggles the completion status of a todo.

- **Inputs**: `_id` (Todo ID)
- **Access**: Public (Restricted to the owner)

---

### `removeTodo(uint256 _id)`

Removes a todo from the list.

- **Inputs**: `_id` (Todo ID)
- **Access**: Public (Restricted to the owner)
- **Emits**: `RemoveEvent`

---

### `getTodoById(uint256 _id) private view returns (Todo memory, uint256 index)`

Finds a todo by ID for internal use.

- **Inputs**: `_id` (Todo ID)
- **Outputs**: The `Todo` struct and its index in the array.

---

## Deployment

1. Compile the contract using [Remix](https://remix.ethereum.org/) or your preferred Solidity development environment.
2. Deploy the contract to a blockchain network (e.g., Ethereum or a testnet).

---

## Usage

### Example Workflow

1. **Create Todo**: Call `createTodo` with a description.
2. **Retrieve Todos**: Use `getTodos` to view all your todos.
3. **Update Todo**: Modify a todo by calling `updateTodo` with the todo ID and new description.
4. **Toggle Completion**: Mark a todo as completed or incomplete using `toggleComplete`.
5. **Remove Todo**: Delete a todo using `removeTodo`.

---

## Example Interaction

### Create a Todo

```solidity
createTodo("Learn Solidity");
