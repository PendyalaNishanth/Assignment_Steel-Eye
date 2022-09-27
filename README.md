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

https://github.com/PendyalaNishanth/new_code/blob/main/React.js


