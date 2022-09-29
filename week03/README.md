# Week 3

## Build Search Filter In React

DESCRIPTION:

React code to build a simple search filter functionality to display a filtered list based on the search query entered by the user.

## Example

![example](https://media.giphy.com/media/LOKDh60aCvDk6FByLq/giphy.gif)

Solution:

``` jsx
import { useState } from "react";

export const Search = () => {
  const list = [
    "Banana",
    "Apple",
    "Orange",
    "Mango",
    "Pineapple",
    "Watermelon",
  ];

  const [filterList, setFilterList] = useState(list);

  const handleSearch = (event) => {
    const text = event.target.value.toLowerCase();

    if (text.length === 0) {
      setFilterList(list);
      return true;
    }

    const newList = list.filter((element) => {
      return element.toLowerCase().indexOf(text) !== -1;
    });

    setFilterList(newList);
  };

  return (
    <>
      <input type="text" onChange={handleSearch} />
      {filterList.map((element) => {
        return <div>{element}</div>;
      })}
    </>
  );
};
```