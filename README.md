# SteelEye-Frontend-Assignment
# SteelEye Frontend Engineer Assignment
#### Introduction
##### Based on the code below answer the following queries:
- Explain what the simple List component does.
- What problems / warnings are there with code?(Attached with github repository).
- Please fix, optimize, and/or modify the component as much as you think is necessary.
#### SOLUTION:-

##### Explain what the simple List component does.
- : Lists are used to display data in an ordered format and mainly used to display menus on websites. The map() function is used for traversing the lists. It is basically allows you to display a list of pages or links by defining a parent page .
##### What problems / warnings are there with code?
``` src\App.js
  Line 39:6:  React Hook useEffect has a missing dependency: 'setSelectedIndex'. Either include it or remove the dependency array  react-hooks/exhaustive-deps

Search for the keywords to learn more about each warning.
To ignore, add // eslint-disable-next-line to the line before.

WARNING in [eslint]
src\App.js
  Line 39:6:  React Hook useEffect has a missing dependency: 'setSelectedIndex'. Either include it or remove the dependency array  react-hooks/exhaustive-deps

webpack compiled with 1 warning 
```
And many more Warning while debugging the code It has been discussed in below qustion with solution to tagle them.

##### Please fix, optimize, and/or modify the component as much as you think is necessary.
- `Parameters` Passed in const [setSelectedIndex,selectedIndex ] = useState(null); is missed placed. Just swapping the Parameters solves an error
- Removing  index from the following
    - `WrappedSingleListItem.`
    - `WrappedSingleListItem.propTypes`
- There was error in return function where index was pass instead of key to correct That I have replaced `index` with `key`. 
- Also in return function the onClick should not pass now index as argument because it has already been removed it should be set to `onClick={onClickHandler}`
- In `WrappedListComponent.propTypes` shapeof should to corrected to `shape` also array of object should be defined as `arrayOf(object)`.

### Final CODE After Debugging And Output
```JAVASCRIPT
import React, { useState, useEffect, memo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
  //index,//remove index
  isSelected,
  onClickHandler,
  text,
}) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={onClickHandler}//onClickHandler(index) -> onClickHandler
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  //index: PropTypes.number,//remove index
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [selectedIndex, setSelectedIndex] = useState(null);

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = index => {
    setSelectedIndex(index);
  };

  return (
    <ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          onClickHandler={() => handleClick(index)}
          text={item.text}
          key={index}//rename index to key
          isSelected={selectedIndex === index}
        />
      ))}
    </ul>
  )
};

WrappedListComponent.propTypes = {
  items: PropTypes.array(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};
//shapeof -> shape
WrappedListComponent.defaultProps = {
  items: null,
};

const List = memo(WrappedListComponent);

export default List;
```


# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)

![image](https://user-images.githubusercontent.com/54151576/193424913-fb074339-18fe-4928-a973-a69083aaa069.png)
![image](https://user-images.githubusercontent.com/54151576/193424931-8389423e-58e3-45c1-a5d9-95c1768fa6ca.png)
![image](https://user-images.githubusercontent.com/54151576/193424940-1f9d7242-f800-42d4-b2d2-d369c490a44e.png)
![image](https://user-images.githubusercontent.com/54151576/193424955-716fcbdf-b8f4-4069-a90c-16956edc4c1a.png)
![image](https://user-images.githubusercontent.com/54151576/193424963-51d5b11a-bb24-4150-a7c8-f2e192bbb676.png)

