# Assignment_Steel-Eye

Q1) Explain what the simple List component does.
List Component is used to display List with some texts as List items. The wrappedListComponent returns a memorized components list. It  accepts an array of objects as props. Each object in this list has a text property. The List component renders the value of the text property of all the elements present in the list prop as an unordered list. For each items in the array, it maps through all and displays their content on the screen with a background color. By default, each element of the unordered list has a red background which changes to green when the element is clicked. This behavior might be used to tell the user that a particular element is being selected. 


Q2) What problems / warnings are there with code?

-> array should be arrayOf as we are defining type of array elements as well. shapeOf should be shape(syntax error).
 WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};

-> When we use useState its take two perimeters. first is variable and second is a function.
const [selectedIndex, setSelectedIndex] = useState();

-> Passing a number selectedIndex to isSelected which should be a bool
<ul style={{ textAlign: "left" }}>
       {items.map((item, index) => (
        <SingleListItem
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={selectedIndex}
        />
      ))}
</ul>

-> We should not define a default prop as null, not recommended.
WrappedListComponent.defaultProps = {
  items: null,
};

-> The calling functionality is wrong it should be 
WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(
    PropTypes.shape({
      text: PropTypes.string.isRequired,
    })
  ),
};


Q3) Please fix, optimize, and/or modify the component as much as you think is necessary.

import React, { useState, useEffect, memo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
    index,
    isSelected,
    onClickHandler,
    text,
}) => {
    return (
        <li
            style={{ backgroundColor: isSelected ? 'green' : 'red' }}
            onClick={() => onClickHandler(index)}
        >
            {text}
        </li>
    );
};

WrappedSingleListItem.propTypes = {
    index: PropTypes.number,
    isSelected: PropTypes.bool,
    onClickHandler: PropTypes.func.isRequired,
    text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({ items, }) => {

    const [selectedIndex, setSelectedIndex] = useState();

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
                    key={index}
                    onClickHandler={() => handleClick(index)}
                    text={item.text}
                    index={index}                    
                    isSelected={Boolean(selectedIndex)}
                />
            ))}
        </ul>
    )
};

WrappedListComponent.propTypes = {
    items: PropTypes.arrayOf(PropTypes.shape({
        text: PropTypes.string.isRequired,
    }).isRequired
    ).isRequired
};

WrappedListComponent.defaultProps = {
    items: undefined 
};

const List = memo(WrappedListComponent);

export default List;

