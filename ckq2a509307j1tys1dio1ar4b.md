# 18- Building a dialog box

Building a dialog box to asking want to save changes:
```
qmb = QMessageBox()
qmb.setText('Want to save your changes?')
qmb.setStandardButtons(QMessageBox.Save | QMessageBox.Discard | QMessageBox.Cancel)
return_value = qmb.exec()

if return_value == QMessageBox.Save:
    print("You pressed Save")
elif return_value == QMessageBox.Discard:
    print("You pressed Discard")
else:
    print('You pressed Cancel')
```