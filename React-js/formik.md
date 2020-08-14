# Using *`FORMIK`* with *`React js`*

Formik is an open source **form** library for React.

It is a small group of React components and hooks for building forms in React and React Native. It helps with the three most annoying parts:

- Getting values in and out of form state
- Validation and error messages
- Handling form submission

## Installation

`npm install formik --save`

or

`yarn add formik`

---

## using `<Formik />`

`<Formik>` is a component that helps you with building forms.

```
<Formik
    initialValues={{
        somefield: ""
    }}
    
    onSubmit={ someSubmitLogic }
    >
    { props => (
        <form onSubmit={ props.handleSubmit }>
            <input
                type="text"
                onChange={props.handleChange}
                onBlur={props.handleBlur}
                value={props.values.name}
                name="name"
                />
            <button type="submit">submit</button>
        </form>
    )}
</Formik>
```

### using `<Field />`

you can use `<Field />` inside the `<form>` as `<input />` field
```
<form onSubmit={ props.handleSubmit }>
    <Field name="name"/>
    <button type="submit">submit</button>
</form>
```

---
## a simple sign up form component using formik

```
import React from 'react';
import { Formik, Field } from 'formik';

function onsubmit(values){
  console.log(values);
}

const form = (props) => {
  return (
    <form onSubmit={ props.handleSubmit }>
      <label>Name </label>
      <Field name="name"/><br/>
      <label>Mail </label>
      <Field name="mail" type="email"/><br/>
      <label>select something</label>
      <Field name="selectDrop" component="select">
        <option value="1">option One</option>
        <option value="2">option Two</option>
        <option value="3">option Three</option>
      </Field><br/>
      <label>check if something</label>
      <Field name="checkBox" type="checkbox" /><br/>
      <label>choose an option: </label> <br/>
      <Field name="selectOne" type="radio" value="1"/> option 1 <br/>
      <Field name="selectOne" type="radio" value="2"/> option 2 <br/>
      <button type="submit">sign up</button>
    </form>
  )
}

function SignUpForm() {
    return <div>
      <h1>Sign Up</h1>
      <Formik
        initialValues={{
          name: "",
          mail: "",
          selectDrop: "1",
          checkBox: false,
          selectOne: ""
        }}
        
        onSubmit={ onsubmit }
        >
        { form }
      </Formik>
    </div>
}

export default SignUpForm;
```
---
## Validation & ErrorMessage

In formik validation is left up to you. so feel free to write your own validators or use a 3rd party library. they recommend using **`Yup`** for object schema validation.

### Installation

`npm install yup --save`


### using with our sign up form example

```
import React from 'react';
import { Formik, Field, ErrorMessage } from 'formik';
import * as Yup from 'yup'

function onsubmit(values){
  console.log(values);
}

function schema(){
  const schema = Yup.object().shape({
    name: Yup.string().min(2, 'Too Short!').max(50, 'Too Long!').required('Required'),
    mail: Yup.string().email('Invalid email').required('Required'),
    selectOne: Yup.string().required('choose is Required')
  });

  return schema;
}

const form = (props) => {
  return (
    <form onSubmit={ props.handleSubmit }>
      <label>Name </label>
      <Field name="name"/><br/>
      <ErrorMessage name="name" /> <br/>

      <label>Mail </label>
      <Field name="mail" type="email"/><br/>
      <ErrorMessage name="mail" /> <br/>

      <label>select something</label>
      <Field name="selectDrop" component="select">
        <option value="1">option One</option>
        <option value="2">option Two</option>
        <option value="3">option Three</option>
      </Field><br/>

      <label>check if something</label>
      <Field name="checkBox" type="checkbox" /><br/>

      <label>choose an option: </label> <br/>
      <Field name="selectOne" type="radio" value="1"/> option 1 <br/>
      <Field name="selectOne" type="radio" value="2"/> option 2 <br/>
      <ErrorMessage name="selectOne" /> <br/>
      
      <button type="submit">sign up</button>
    </form>
  )
}

function SignUpForm() {
    return <div>
      <h1>Sign Up</h1>
      <Formik
        initialValues={{
          name: "",
          mail: "",
          selectDrop: "1",
          checkBox: false,
          selectOne: ""
        }}
        
        onSubmit={ onsubmit }

        validationSchema={ schema() }
        >
        { form }
      </Formik>
    </div>
}

export default SignUpForm;
```
---

## nested objects

```
import React from 'react';
import { Formik, Field, ErrorMessage } from 'formik';
import * as Yup from 'yup'

function onsubmit(values){
  console.log(values);
}

function schema(){
  const schema = Yup.object().shape({
    name: Yup.string().min(2, 'Too Short!').max(50, 'Too Long!').required('Required'),
    mail: Yup.string().email('Invalid email').required('Required'),
    selectOne: Yup.string().required('choose is Required'),
    nestedObject : Yup.object().shape({
      fieldOne: Yup.string().required(),
      fieldTwo: Yup.string().required()
    })
  });

  return schema;
}

const form = (props) => {
  return (
    <form onSubmit={ props.handleSubmit }>
      <label>Name </label>
      <Field name="name"/><br/>
      <ErrorMessage name="name" /> <br/>

      <label>Mail </label>
      <Field name="mail" type="email"/><br/>
      <ErrorMessage name="mail" /> <br/>

      <label>select something</label>
      <Field name="selectDrop" component="select">
        <option value="1">option One</option>
        <option value="2">option Two</option>
        <option value="3">option Three</option>
      </Field><br/>

      <label>check if something</label>
      <Field name="checkBox" type="checkbox" /><br/>

      <label>choose an option: </label> <br/>
      <Field name="selectOne" type="radio" value="1"/> option 1 <br/>
      <Field name="selectOne" type="radio" value="2"/> option 2 <br/>
      <ErrorMessage name="selectOne" /> <br/>

      <label>Nested Field One </label>
      <Field name="nestedObject.fieldOne"/><br/>
      <ErrorMessage name="nestedObject.fieldOne" /> <br/>

      <label>Nested Field Two </label>
      <Field name="nestedObject.fieldTwo"/><br/>
      <ErrorMessage name="nestedObject.fieldTwo" /> <br/>
      
      <button type="submit">sign up</button>
    </form>
  )
}

function SignUpForm() {
    return <div>
      <h1>Sign Up</h1>
      <Formik
        initialValues={{
          name: "",
          mail: "",
          selectDrop: "1",
          checkBox: false,
          selectOne: "",
          nestedObject: {
            fieldOne: "",
            fieldTwo: ""
        }}}
        
        onSubmit={ onsubmit }

        validationSchema={ schema() }
        >
        { form }
      </Formik>
    </div>
}

export default SignUpForm;
```

---
## Array of object using **`<FieldArray/>`**

the following example contain a full form with different fields to customize 

```
import React from 'react';
import { Formik, Field, ErrorMessage, FieldArray } from 'formik';
import * as Yup from 'yup'

function onsubmit(values){
  console.log(values);
}

function schema(){
  const schema = Yup.object().shape({
    name: Yup.string().min(2, 'Too Short!').max(50, 'Too Long!').required('Required'),
    mail: Yup.string().email('Invalid email').required('Required'),
    selectOne: Yup.string().required('choose is Required'),
    subForm: Yup.array().of(
      Yup.object().shape({
        name: Yup.string().min(2, 'Too Short!').max(50, 'Too Long!').required('Required'),
        phone: Yup.number().typeError('accept numbers only').required('Required')
      })
    )
  });

  return schema;
}

const form = (props) => {
  return (
    <form onSubmit={ props.handleSubmit }>
      <label>Name </label>
      <Field name="name"/><br/>
      <ErrorMessage name="name" /> <br/>

      <label>Mail </label>
      <Field name="mail" type="email"/><br/>
      <ErrorMessage name="mail" /> <br/>

      <label>select something</label>
      <Field name="selectDrop" component="select">
        <option value="1">option One</option>
        <option value="2">option Two</option>
        <option value="3">option Three</option>
      </Field><br/>

      <label>check if something</label>
      <Field name="checkBox" type="checkbox" /><br/>

      <label>choose an option: </label> <br/>
      <Field name="selectOne" type="radio" value="1"/> option 1 <br/>
      <Field name="selectOne" type="radio" value="2"/> option 2 <br/>
      <ErrorMessage name="selectOne" /> <br/>

      <FieldArray 
        name="subForm"
        render={ arrayHelpers => (
          <div>
            <h2>Contacts </h2>
            { props.values.subForm.map((item, index) => (
              <div key="index">

                <label>name </label>
                <Field name={`subForm[${index}].name`}/>
                <ErrorMessage name={`subForm[${index}].name`} /><br />
                <label> phone </label>
                <Field name={`subForm[${index}].phone`}/>
                <ErrorMessage name={`subForm[${index}].phone`} /><br />

                <button type="button" onClick={ () => { arrayHelpers.remove(index)} } > 
                  remove 
                </button> <br />
              </div>
            ))}

            <button type="button" onClick={()=>arrayHelpers.push({name:'', phone: ''})}>
              Add Contact
            </button>
          </div>
        )}
        />
      
      <button type="submit">sign up</button>
    </form>
  )
}

function SignUpForm() {
    return <div>
      <h1>Sign Up</h1>
      <Formik
        initialValues={{
          name: "",
          mail: "",
          selectDrop: "1",
          checkBox: false,
          selectOne: "",
          subForm: [
            {
              name: "",
              phone: ""
        }}}
        
        onSubmit={ onsubmit }

        validationSchema={ schema() }
        >
        { form }
      </Formik>
    </div>
}

export default SignUpForm;

```
---

previous: [forms](form.md)

Next: []()