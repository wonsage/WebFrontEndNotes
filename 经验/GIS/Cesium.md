## Viewer
### dataSourceDisplay
一个[DataSourceDisplay]([DataSourceDisplay - Cesium Documentation](http://cesium.xin/cesium/cn/Documentation1.95/DataSourceDisplay.html))对象
- dataSources
- defaultDataSource
###  dataSources
一个DataSourceCollection对象，指向dataSourceDisplay.dataSources
DataSource一般会添加到这里。
### entities
viewer.entites指向dataSourceDisplay.defaultDataSource.entities
一般用于存放未加分类的实体。

### scene
场景
- imgerLaters
- camera
### imagerLaters
指向scene.imgerLaters
## 其他
### 如何对dataSource管理
新的dataSource会加到viewer.dataSources中，同一类dataSource设为同样的name，然后使用DataSourceCollection.getByName()获取所有匹配的。