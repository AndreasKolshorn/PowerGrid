# Power Grid

## Features
* blazing fast performance and massive scale (100M cells+) via virtualized viewport
* React interface
* completely customizable cells via JSX and CSS
* cell interactivity
* expand / collapse rows and columns
* merged cells support (colspans and rowspans)
* dynamic row heights and column widths
* native scroll bars
* any number of fixed rows and headers
* screen reader accessible via semantic table html

## React Cell JSX Example (MyCell)


```JSX
const React = require('react');

module.exports = (props) => {
  let viewModel = props.viewModel;
  return (
    <td className={'power-grid-cell power-grid-my-cell ' + viewModel.rating} onClick={props.onClick} data-row={props.row} style={{transform: 'translate(' + props.x + 'px,' + props.y + 'px)', width: (props.width-2)+'px', height: props.height+'px'}}>
      {viewModel.value}
    </td>
  )
}
```

## React Cell SCSS Example

```SCSS
.power-grid-cell.power-grid-my-cell {
  background-color: #eee;

  &.bad {
    background-color: #ffc7ce;
    color: #9c0006;
  }

  &.neutral {
    background-color: #ffeb9c;
    color: #9c5700;
  }

  &.good {
    background-color: #c6efce;
    color: #267c27;
  }

  &:hover {
    background-color: #b0d9fe;
  }
}
```

## View Model Example 

```javascript
let viewModel = {
  hideScrollbars: false,
  maxCellsWhileScrolling: 1000,
  x: 0,
  y: 0,
  width: 200,
  height: 100,
  colWidths: [100, 120],
  rowHeights: [80, 60],
  // row based.  array of rows, and each row is an array of cells
  cells: [
    [
      {
        renderer: MyCell,
        viewModel: {
          value: 5,
          rating: 'good'
        }
      },
      {
        renderer: MyCell,
        viewModel: {
          value: 5,
          rating: 'good'
        }
      }
    ],
    [
      {
        renderer: MyCell,
        viewModel: {
          value: 5,
          rating: 'good'
        }
      },
      {
        renderer: MyCell,
        viewModel: {
          value: 2,
          rating: 'bad'
        }
      }
    ]
  ]
}
```

## Simple App Example

```JSX
<PowerGrid viewModel={viewModel} onViewModelUpdate={onViewModelUpdate} onCellClick={onCellClick}/>
```

## Fixed Row Headers and Col Headers App Example

```JSX
  ReactDom.render(
    <div className="example-grid">
      <div className="top">
        <div className="left">
        </div>
        <div className="col-headers">
          <PowerGrid viewModel={colHeadersViewModel}/>
        </div>  
      </div>
      <div className="bottom">
        <div className="row-headers">
          <PowerGrid viewModel={rowHeadersViewModel}/>
        </div>
        <div className="main-grid">
          <PowerGrid viewModel={mainViewModel} onViewModelUpdate={onViewModelUpdate} onCellClick={onCellClick}/>
        </div>
      </div>
    </div>
    , appContainer);
```