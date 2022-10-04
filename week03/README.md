# Week 3

## Build Search Filter In React

DESCRIPTION:

React code to build a simple search filter functionality to display a filtered list based on the search query entered by the user.

## Example

![example](https://media.giphy.com/media/LOKDh60aCvDk6FByLq/giphy.gif)

Solution:

```jsx
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

## Fetch Random User Data

DESCRIPTION:

React code to fetch from this API random users. You should display the Name, website, email and phone of a random user. Also there should be a Reset button to fetch a new user (For this you need to generate a random number from 1 to 10).

Solution:

``` jsx
import React from 'react';
import './style.css';

export default function App() {
  const [userData, setUserData] = React.useState({});

  const getUserData = async () => {
    const randomNumber = Math.floor(Math.random() * 10) + 1;
    const url = `https://randomuser.me/api/`;
    const response = await fetch(url);
    const data = await response.json();
    const jsonData = {
      name: data.results[0].name.first + ' ' + data.results[0].name.last,
      website: data.results[0].picture.large,
      email: data.results[0].email,
      phone: data.results[0].phone,
    };
    setUserData(jsonData);
  };

  React.useEffect(() => {
    getUserData();
  }, []);

  const reset = async () => {
    await getUserData();
  };

  return (
    <div className="App">
      <button onClick={() => reset()}>Reset</button>
      <h2>User Data</h2>

      <p>
        <strong>Name:</strong> {userData.name}
      </p>
      <p>
        <strong>Website:</strong> {userData.website}
      </p>
      <p>
        <strong>Email:</strong> {userData.email}
      </p>
      <p>
        <strong>Phone:</strong> {userData.phone}
      </p>
    </div>
  );
}
```