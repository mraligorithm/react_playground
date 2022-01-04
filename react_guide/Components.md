# Components
Components are independent and reusable bits of code. They serve the same purpose as JavaScript functions, but work in isolation and return HTML.

Components come in two types, Class components and Function components, in this tutorial we will concentrate on Function components.

## Class Component

A class component must include the extends React.Component statement. This statement creates an inheritance to React.Component, and gives your component access to React.Component's functions.

The component also requires a render() method, this method returns HTML.

```
class Car extends React.Component {
  render() {
    return <h2>Hi, I am a Car!</h2>;
  }
}
```

## Function Component

Here is the same example as above, but created using a Function component instead.

A Function component also returns HTML, and behaves much the same way as a Class component, but Function components can be written using much less code, are easier to understand, and will be preferred in this tutorial.

```
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}
```

## Rendering a Component

Now your React application has a component called Car, which returns an <h2> element.

To use this component in your application, use similar syntax as normal HTML: <Car />

`ReactDOM.render(<Car />, document.getElementById('root'));`

# Props
Props are arguments passed into React components.

Props are passed to components via HTML attributes.

Components can be passed as props, which stands for properties.

Props are like function arguments, and you send them into the component as attributes.


```
function Car(props) {
  return <h2>I am a {props.color} Car!</h2>;
}

ReactDOM.render(<Car color="red"/>, document.getElementById('root'));
```

## Components in Components

```
function Car() {
  return <h2>I am a Car!</h2>;
}

function Garage() {
  return (
    <>
      <h1>Who lives in my Garage?</h1>
      <Car />
    </>
  );
}

ReactDOM.render(<Garage />, document.getElementById('root'));
```


```
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.js
        import React from 'react';

        import Expenses from './components/Expenses/Expenses';

        const App = () => {
          const expenses = [
            {
              id: 'e1',
              title: 'Toilet Paper',
              amount: 94.12,
              date: new Date(2020, 7, 14),
            },
            { id: 'e2', title: 'New TV', amount: 799.49, date: new Date(2021, 2, 12) },
            {
              id: 'e3',
              title: 'Car Insurance',
              amount: 294.67,
              date: new Date(2021, 2, 28),
            },
            {
              id: 'e4',
              title: 'New Desk (Wooden)',
              amount: 450,
              date: new Date(2021, 5, 12),
            },
          ];

          return (
            <div>
              <h2>Let's get started!</h2>
              <Expenses items={expenses} />
            </div>
          );
        }

        export default App;
    ├── components
    │   ├── Expenses
    │   │   ├── ExpenseDate.css
                .expense-date {
                  display: flex;
                  flex-direction: column;
                  width: 5.5rem;
                  height: 5.5rem;
                  border: 1px solid #ececec;
                  background-color: #2a2a2a;
                  color: white;
                  border-radius: 12px;
                  align-items: center;
                  justify-content: center;
                }

                .expense-date__month {
                  font-size: 0.75rem;
                  font-weight: bold;
                }

                .expense-date__year {
                  font-size: 0.75rem;
                }

                .expense-date__day {
                  font-size: 1.5rem;
                  font-weight: bold;
                }

    │   │   ├── ExpenseDate.js
            import React from "react";

            import "./ExpenseDate.css";

            const ExpenseDate = (props) => {
              const month = props.date.toLocaleString("en-US", { month: "long" });
              const day = props.date.toLocaleString("en-US", { day: "2-digit" });
              const year = props.date.getFullYear();

              return (
                <div className="expense-date">
                  <div className="expense-date__month">{month}</div>
                  <div className="expense-date__year">{year}</div>
                  <div className="expense-date__day">{day}</div>
                </div>
              );
            };

            export default ExpenseDate;

    │   │   ├── ExpenseItem.css
            .expense-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem;
            margin: 1rem 0;
            background-color: #4b4b4b;
          }

          .expense-item__description {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            align-items: flex-end;
            flex-flow: column-reverse;
            justify-content: flex-start;
            flex: 1;
          }

          .expense-item h2 {
            color: #3a3a3a;
            font-size: 1rem;
            flex: 1;
            margin: 0 1rem;
            color: white;
          }

          .expense-item__price {
            font-size: 1rem;
            font-weight: bold;
            color: white;
            background-color: #40005d;
            border: 1px solid white;
            padding: 0.5rem;
            border-radius: 12px;
          }

          @media (min-width: 580px) {
            .expense-item__description {
              flex-direction: row;
              align-items: center;
              justify-content: flex-start;
              flex: 1;
            }

            .expense-item__description h2 {
              font-size: 1.25rem;
            }

            .expense-item__price {
              font-size: 1.25rem;
              padding: 0.5rem 1.5rem;
            }
          }
    │   │   ├── ExpenseItem.js
            import React from 'react';

            import ExpenseDate from './ExpenseDate';
            import Card from '../UI/Card';
            import './ExpenseItem.css';

            const ExpenseItem = (props) => {
              return (
                <Card className='expense-item'>
                  <ExpenseDate date={props.date} />
                  <div className='expense-item__description'>
                    <h2>{props.title}</h2>
                    <div className='expense-item__price'>${props.amount}</div>
                  </div>
                </Card>
              );
            }

            export default ExpenseItem;

    │   │   ├── Expenses.css
            .expenses {
              padding: 1rem;
              background-color: rgb(31, 31, 31);
              margin: 2rem auto;
              width: 50rem;
              max-width: 95%;
            }

    │   │   └── Expenses.js
            import React from 'react';

            import ExpenseItem from './ExpenseItem';
            import Card from '../UI/Card';
            import './Expenses.css';

            const Expenses = (props) => {
              return (
                <Card className="expenses">
                  <ExpenseItem
                    title={props.items[0].title}
                    amount={props.items[0].amount}
                    date={props.items[0].date}
                  />
                  <ExpenseItem
                    title={props.items[1].title}
                    amount={props.items[1].amount}
                    date={props.items[1].date}
                  />
                  <ExpenseItem
                    title={props.items[2].title}
                    amount={props.items[2].amount}
                    date={props.items[2].date}
                  />
                  <ExpenseItem
                    title={props.items[3].title}
                    amount={props.items[3].amount}
                    date={props.items[3].date}
                  />
                </Card>
              );
            }

            export default Expenses;

    │   └── UI
    │       ├── Card.css
            .card {
              border-radius: 12px;
              box-shadow: 0 1px 8px rgba(0, 0, 0, 0.25);
            }

    │       └── Card.js
            import React from 'react';

            import './Card.css';

            const Card = (props) => {
              const classes = 'card ' + props.className;

              return <div className={classes}>{props.children}</div>;
            };

            export default Card;

    ├── index.css
    └── index.js
