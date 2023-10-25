---
category: examples
group: table-type
title: 透视分析表格
cover: https://lf9-dp-fe-cms-tos.byteorg.com/obj/bit-cloud/VTable/preview/pivot-analysis-table-tree.png
link: '../guide/table_type/Pivot_table/pivot_table_dataAnalysis'
---

# 透视分析表格树形展示

透视分析表格树形展示

## 关键配置

- `PivotTable`
- `rowHierarchyType` 将层级展示设置为`tree`，默认为平铺模式`grid`。
- `columns` 
- `rows`
- `indicators`
- `enableDataAnalysis` 开启透视数据分析
- `dataConfig` 配置数据规则，可选配置项
## 代码演示

```javascript livedemo template=vtable

let  tableInstance;
  fetch('https://lf9-dp-fe-cms-tos.byteorg.com/obj/bit-cloud/VTable/North_American_Superstore_Pivot_Chart_data.json')
    .then((res) => res.json())
    .then((data) => {

const option = {
records:data,
  "rows": [
      {
         "dimensionKey": "Category",
          "title": "Category",
          "headerStyle": {
              "textStick": true
          },
          "width": "auto",
      },
      {
         "dimensionKey": "Sub-Category",
          "title": "Sub-Catogery",
          "headerStyle": {
              "textStick": true
          },
          "width": "auto",
      },
  ],
  "columns": [
      {
         "dimensionKey": "Region",
          "title": "Region",
          "headerStyle": {
              "textStick": true
          },
          "width": "auto",
      },
       {
         "dimensionKey": "Segment",
          "title": "Segment",
          "headerStyle": {
              "textStick": true
          },
          "width": "auto",
      },
  ],
  "indicators": [
              {
                  "indicatorKey": "Quantity",
                  "title": "Quantity",
                  "width": "auto",
                  "showSort": false,
                  "headerStyle":{
                    fontWeight: "normal",
                  },
                   style:{
                    padding:[16,28,16,28],
                    color(args){
                      if(args.dataValue>=0)
                      return 'black';
                      return 'red'
                    }
                   }
              },
              {
                  "indicatorKey": "Sales",
                  "title": "Sales",
                  "width": "auto",
                  "showSort": false,
                  "headerStyle":{
                    fontWeight: "normal",
                  },
                  "format":(rec)=>{return '$'+Number(rec).toFixed(2)},
                  style:{
                    padding:[16,28,16,28],
                    color(args){
                      if(args.dataValue>=0)
                      return 'black';
                      return 'red'
                    }
                   }
              },
              {
                  "indicatorKey": "Profit",
                  "title": "Profit",
                  "width": "auto",
                  "showSort": false,
                  "headerStyle":{
                    fontWeight: "normal",
                  },
                  "format":(rec)=>{return '$'+Number(rec).toFixed(2)},
                  style:{
                    padding:[16,28,16,28],
                    color(args){
                      if(args.dataValue>=0)
                      return 'black';
                      return 'red'
                    }
                   }
              }
          ],
  "corner": {
      "titleOnDimension": "row",
      "headerStyle": {
          "textStick": true
      }
  },
  dataConfig: {
    sortRules: [
      {
        sortField: 'Category',
        sortBy: ['Office Supplies', 'Technology','Furniture']
      }
    ],
    totals: {
        row: {
          showSubTotals: true,
          subTotalsDimensions: ['Category'],
          subTotalLabel: 'subtotal'
        }
      }
  },
  enableDataAnalysis: true,
  rowHierarchyType: 'tree',
  widthMode:'standard'
};
tableInstance = new VTable.PivotTable(document.getElementById(CONTAINER_ID),option);
window['tableInstance'] = tableInstance;
    })
```