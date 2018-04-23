# dxDataGrid - How to implement cascading lookup columns


This example demonstrates how to implement cascading lookup columns using the dxDataGrid widget. To accomplish this task, we need to perform the following steps:<br><br>1. Reset a value in a cell of the second lookup column (the <strong>Product</strong> column) when a cell value in the first lookup column (the <strong>Category</strong> column) is changed. We need to use the <a href="http://js.devexpress.com/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/columns/?version=15_2#setCellValue">dxDataGrid.columns.setCellValue</a> callback function for this. This function accepts two parameters. The first one is data of the current row, and the second one is the inputed value. So, our code should be as follows:<br>


```js
{
    dataField: 'Category',    
    setCellValue: function (rowData, value) {
        rowData.Product = null;
        this.defaultSetCellValue(rowData, value);
    },
    ...
}
```


<br>
<p>2. We need to filter values for a cell in the second lookup column based on the current value from the first column. In this case, we can specify the <a href="http://js.devexpress.com/Documentation/ApiReference/UI_Widgets/dxDataGrid/Configuration/columns/lookup/?version=15_2#dataSource">dxDataGrid.columns.lookup.dataSource</a> option as a callback function. This function must return a data source configuration object and we can specify the filter expression for our data source based on the current value of the first lookup column. The data option will help us to do this. So, the code should be as follows:</p>


```js
{
    dataField: 'Product',
    lookup: {
        dataSource: function (options) {
            var dataSourceConfiguration = {
                store: products
            };
            if (options.data) {
                dataSourceConfiguration.filter = ['CategoryID', '=', options.data.Category];
            }
            return dataSourceConfiguration;
        },
        ...
    }
}
```


<br><strong>See also:</strong><br><a href="https://www.devexpress.com/Support/Center/p/E5000">How to implement cascading lookups</a>

<br/>


