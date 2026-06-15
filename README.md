# How-to-Add-an-Error-Indicator-Using-CustomPainter-in-Flutter-DataTable

In this article, we will show how to add an error indicator using a CustomPainter in a [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all the required configurations. To display an error indicator in a cell corner, customize the [DataGridSource.buildRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/buildRow.html) method and leverage the [CustomPainter](https://api.flutter.dev/flutter/rendering/CustomPainter-class.html) feature.

In this approach, each cell is wrapped inside a [Stack](https://api.flutter.dev/flutter/widgets/Stack-class.html) widget, which allows the base content and the error indicator to be layered together. The main cell content is placed at the bottom, while the indicator is positioned on top using a [Positioned](https://api.flutter.dev/flutter/widgets/Positioned-class.html) widget.

You can apply conditional logic inside the `buildRow` method to control when the error indicator should be displayed (for example, based on a specific column value). The `CustomPainter` is then used to draw a visual indicator, such as a red triangle, in the top-right corner of the cell.

```dart
  @override
  DataGridRowAdapter buildRow(DataGridRow row) {
    return DataGridRowAdapter(
      cells: row.getCells().map<Widget>((e) {
        return Stack(
          children: [
            // Existing cell content
            Container(
              alignment: Alignment.center,
              padding: EdgeInsets.all(8.0),
              child: Text(e.value.toString()),
            ),

            // Error indicator (top-right)
            if (e.columnName == 'salary' &&
                e.value <= 15000) // <-- Add your condition here
              Positioned(
                top: 0,
                right: 0,
                child: CustomPaint(
                  size: Size(15, 15), // Indicator size
                  painter: ErrorIndicatorPainter(),
                ),
              ),
          ],
        );
      }).toList(),
    );
  }

```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-Add-an-Error-Indicator-Using-CustomPainter-in-Flutter-DataTable).

