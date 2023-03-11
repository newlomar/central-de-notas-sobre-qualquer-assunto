# React Forms

Basic form example

```js
import React from "react";

export default function Form() {
  const [formData, setFormData] = React.useState({
    firstName: "",
    lastName: "",
    email: "",
    comments: "",
    isFriendly: true,
    employment: "",
    favColor: "",
  });

  function handleChange(event) {
    const { name, value, type, checked } = event.target;
    setFormData((prevFormData) => {
      return {
        ...prevFormData,
        [name]: type === "checkbox" ? checked : value,
      };
    });
  }

  function handleSubmit(event) {
    event.preventDefault();
    // submitToApi(formData)
    console.log(formData);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        placeholder="First Name"
        onChange={handleChange}
        name="firstName"
        value={formData.firstName}
      />
      <input
        type="text"
        placeholder="Last Name"
        onChange={handleChange}
        name="lastName"
        value={formData.lastName}
      />
      <input
        type="email"
        placeholder="Email"
        onChange={handleChange}
        name="email"
        value={formData.email}
      />
      <textarea
        value={formData.comments}
        placeholder="Comments"
        onChange={handleChange}
        name="comments"
      />
      <input
        type="checkbox"
        id="isFriendly"
        checked={formData.isFriendly}
        onChange={handleChange}
        name="isFriendly"
      />
      <label htmlFor="isFriendly">Are you friendly?</label>
      <br />
      <br />

      <fieldset>
        <legend>Current employment status</legend>
        <input
          type="radio"
          id="unemployed"
          name="employment"
          value="unemployed"
          checked={formData.employment === "unemployed"}
          onChange={handleChange}
        />
        <label htmlFor="unemployed">Unemployed</label>
        <br />

        <input
          type="radio"
          id="part-time"
          name="employment"
          value="part-time"
          checked={formData.employment === "part-time"}
          onChange={handleChange}
        />
        <label htmlFor="part-time">Part-time</label>
        <br />

        <input
          type="radio"
          id="full-time"
          name="employment"
          value="full-time"
          checked={formData.employment === "full-time"}
          onChange={handleChange}
        />
        <label htmlFor="full-time">Full-time</label>
        <br />
      </fieldset>
      <br />

      <label htmlFor="favColor">What is your favorite color?</label>
      <br />
      <select
        id="favColor"
        value={formData.favColor}
        onChange={handleChange}
        name="favColor"
      >
        <option value="red">Red</option>
        <option value="orange">Orange</option>
        <option value="yellow">Yellow</option>
        <option value="green">Green</option>
        <option value="blue">Blue</option>
        <option value="indigo">Indigo</option>
        <option value="violet">Violet</option>
      </select>
      <br />
      <br />
      <button>Submit</button>
    </form>
  );
}
```

A few questions and answers about Forms:

1. In a vanilla JS app, at what point in the form submission
   process do you gather all the data from the filled-out form?

Right before the submission of the form.

2. In a React app, when do you gather all the data from
   the filled-out form?

As the form is being filled out. The data is all held in local state.

3. Which attribute in the form elements (value, name, onChange, etc.)
   should match the property name being held in state for that input?

name

4. What's different about a saving the data from a checkbox element
   vs. other form elements?

A checkbox uses the `checked` property to determine what should
be saved in state. Other form elements use the `value` property instead.

5. How do you watch for a form submit? How can you trigger
   a form submit?

You can listen to the "submit" event or using the "onSubmit" handler.

You can trigger by clicking a button inside a form. A button inside a form is automatically a submit button

Exercise:

```js
import React from "react";

export default function App() {
  /**
   * Challenge: Connect the form to local state
   *
   * 1. Create a state object to store the 4 values we need to save.
   * 2. Create a single handleChange function that can
   *    manage the state of all the inputs and set it up
   *    correctly
   * 3. When the user clicks "Sign up", check if the
   *    password & confirmation match each other. If
   *    so, log "Successfully signed up" to the console.
   *    If not, log "passwords to not match" to the console.
   * 4. Also when submitting the form, if the person checked
   *    the "newsletter" checkbox, log "Thanks for signing
   *    up for our newsletter!" to the console.
   */

  const [formData, setFormData] = React.useState({
    email: "",
    password: "",
    confirmPassword: "",
    joinNewsletter: false,
  });

  function handleChange(event) {
    const { name, value, type, checked } = event.target;
    setFormData((prevState) => {
      return {
        ...prevState,
        [name]: type === "checkbox" ? checked : value,
      };
    });
  }

  function handleSubmit(event) {
    event.preventDefault();
    const { password, confirmPassword, joinNewsletter } = formData;

    if (password === confirmPassword) {
      console.log("Successfully signed up");
    } else {
      console.log("Passwords do not match");
    }

    if (joinNewsletter) {
      console.log("Thanks for signing up for our newsletter");
    }
  }

  return (
    <div className="form-container">
      <form className="form" onSubmit={handleSubmit}>
        <input
          type="email"
          placeholder="Email address"
          className="form--input"
          name="email"
          onChange={handleChange}
          value={formData.email}
        />
        <input
          type="password"
          placeholder="Password"
          className="form--input"
          name="password"
          onChange={handleChange}
          value={formData.password}
        />
        <input
          type="password"
          placeholder="Confirm password"
          className="form--input"
          name="confirmPassword"
          onChange={handleChange}
          value={formData.confirmPassword}
        />

        <div className="form--marketing">
          <input
            id="okayToEmail"
            type="checkbox"
            name="joinNewsletter"
            onChange={handleChange}
            checked={formData.joinNewsletter}
          />
          <label htmlFor="okayToEmail">I want to join the newsletter</label>
        </div>
        <button className="form--submit">Sign up</button>
      </form>
    </div>
  );
}
```
