---
category: examples
group: data-analysis
title: 指标值排序
cover: https://lf9-dp-fe-cms-tos.byteorg.com/obj/bit-cloud/VTable/preview/pivot-analysis-sort-indicator.png
link: '../guide/table_type/Pivot_table/pivot_table_dataAnalysis'
---

# 透视分析表按指标值排序

透视表按某个维度的维度值进行排序，在dataConfig中配置sortRules，可配置多个排序规则，先配的优先级较高。

## 关键配置

- `PivotTable`
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
              "textStick": true,
              bgColor(arg) {
                if (arg.dataValue === 'Row Totals') {
                  return '#ff9900';
                }
                return '#ECF1F5';
              }
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
                    },
                    bgColor(arg) {
                      const rowHeaderPaths = arg.cellHeaderPaths.rowHeaderPaths;
                      if (rowHeaderPaths?.[1]?.value === 'Sub Totals') {
                        return '#ba54ba';
                      } else if (rowHeaderPaths?.[0]?.value === 'Row Totals') {
                        return '#ff9900';
                      }
                      return undefined;
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
                    },
                     bgColor(arg) {
                      const rowHeaderPaths = arg.cellHeaderPaths.rowHeaderPaths;
                      if (rowHeaderPaths?.[1]?.value === 'Sub Totals') {
                        return '#ba54ba';
                      } else if (rowHeaderPaths?.[0]?.value === 'Row Totals') {
                        return '#ff9900';
                      }
                      return undefined;
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
                    },
                     bgColor(arg) {
                      const rowHeaderPaths = arg.cellHeaderPaths.rowHeaderPaths;
                      if (rowHeaderPaths?.[1]?.value === 'Sub Totals') {
                        return '#ba54ba';
                      } else if (rowHeaderPaths?.[0]?.value === 'Row Totals') {
                        return '#ff9900';
                      }
                      return undefined;
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
        sortField: 'Sub-Category',
          sortByIndicator: 'Sales',
          sortType: VTable.TYPES.SortType.DESC,
          query: ['East', 'Consumer']
      },
      {
        sortField: 'Region',
        sortBy: ['East', 'Central']
      }
    ],
  },
  enableDataAnalysis: true,
  widthMode:'standard'
};
tableInstance = new VTable.PivotTable(document.getElementById(CONTAINER_ID),option);
window['tableInstance'] = tableInstance;
    })
```