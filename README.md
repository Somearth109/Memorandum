# Build a Trello clone with React and Redux 
 
In this project, I have build a note making and messaging app. Where one can make highlights, add notes and drag & drop from various highlights. It provides the user a subtle UI and for user's choice it has a dark theme.



## Dependencies

In this tutorial I have used:
- [redux](https://redux.js.org): to manage the global state of the app
- [react-textarea-autosize](https://github.com/andreypopp/react-textarea-autosize): a react component that will render a textarea that resizes itself when needed
- [react-beautiful-dnd](https://github.com/atlassian/react-beautiful-dnd): A beautiful library to implement drag and drop functionalities
- [lodash.throttle](https://www.npmjs.com/package/lodash.throttle): to prevent too many calls of a function
- [shortid](https://github.com/dylang/shortid): to generate unique ids. 


## Start

Start the app with the following command:

```bash
npm start
```


The structure of my project is:

```
.
├── README.md
├── package-lock.json
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src
    ├── components
    │   └── App.js
    ├── index.css
    ├── index.js
    ├── serviceWorker.js
    └── styles
        └── App.css


## Board reducer

Here redux comes in use when we have to drag and drop a file.

Here the reducer of the board that let us add, move (for the drag and drop) and delete a list id from the array.

`src/store.js`

```javascript
const board = (state = { lists: [] }, action) => {
  switch (action.type) {
    case "ADD_LIST": {
      const { listId } = action.payload;
      return { lists: [...state.lists, listId] };
    }
    case "MOVE_LIST": {
      const { oldListIndex, newListIndex } = action.payload;
      const newLists = Array.from(state.lists);
      const [removedList] = newLists.splice(oldListIndex, 1);
      newLists.splice(newListIndex, 0, removedList);
      return { lists: newLists };
    }
    case "DELETE_LIST": {
      const { listId } = action.payload;
      const filterDeleted = tmpListId => tmpListId !== listId;
      const newLists = state.lists.filter(filterDeleted);
      return { lists: newLists };
    }
    default:
      return state;
  }
};
```

------

