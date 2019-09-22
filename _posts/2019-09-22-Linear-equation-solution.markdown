---
layout:     post
title:      "数值分析之线性方程组求解算法的实现（基于python）"
subtitle:   " \" numerical analysis\""
date:       2019-09-22 18:01:00
author:     "张凡"
header-img: "https://aerozf.oss-cn-beijing.aliyuncs.com/images/frp_network.jpg"
catalog: true
tags:
    - 数值分析
    - Python
---

### 1、列主元高斯消去法

##### 1.1 算法

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/numerical_analysis/lizhuyuanguass.JPG)

##### 1.2 列主元高斯消去法算法的程序实现

```python
def Gauss(Matrix,Matrix_row_num,Matrix_col_num,B):
    G_num=0
    G_time=time.clock()
    A=Matrix
    for k in range(Matrix_row_num-1):
        Max_i_list=[]
        for i in range(k,Matrix_row_num):
            G_num=G_num+1
            Max_i_list.append(A[i][k])
        Max_i=max(Max_i_list)
        Max_i_index=Max_i_list.index(Max_i)+k
        M_t=A[Max_i_index]+0
        A[Max_i_index]=A[k]
        A[k]=M_t
        B_t=B[Max_i_index]
        B[Max_i_index]=B[k]
        B[k]=B_t
        for ii in range(k+1,Matrix_row_num):
            m_ik=A[ii][k]/A[k][k]
            for jj in range(k+1,Matrix_col_num):
                A[ii][jj]=A[ii][jj]-m_ik*A[k][jj]
                G_num=G_num+1
            A[ii][k]=0
            B[ii]=B[ii]-m_ik*B[k]

    '''回带过程'''
    x=[i for i in range(Matrix_row_num)]
    x[Matrix_row_num-1]=B[Matrix_row_num-1]/A[Matrix_row_num-1][Matrix_row_num-1]  #保留小数点后三位
    x[Matrix_row_num-1]=round(x[Matrix_row_num-1],3)
    for k in range(Matrix_row_num-1):
        n=Matrix_row_num-2-k
        s=0
        for j in range(n+1,Matrix_row_num):
            s=s+A[n][j]*x[j]
            G_num=G_num+1
        x[n]=round((B[n]-s)/A[n][n],3)   #保留小数点后三位
    return [list(A),time.clock()-G_time,G_num,x]
```

### 2、Doolittle消去法

##### 2.1 算法

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/numerical_analysis/doolittle.JPG)

##### 2.2 Doolittle消去法算法的程序实现

```python
def Doolittle(Matrix,Matrix_row_num,Matrix_col_num,B):
    G_num=0
    G_time=time.clock()
    A=Matrix
    for k in range(Matrix_row_num):
        for j in range(k,Matrix_row_num):
            s=0
            for t in range(k):
                s=s+A[k][t]*A[t][j]
                G_num=G_num+1
            A[k][j]=Matrix[k][j]-s
        for i in range(k+1,Matrix_row_num):
            if k<Matrix_row_num:
                s=0
                for t in range(k):
                    s=s+A[i][t]*A[t][k]
                    G_num=G_num+1
                A[i][k]=(Matrix[i][k]-s)/A[k][k]
    y=[i for i in range(Matrix_row_num)]
    x=[i for i in range(Matrix_row_num)]
    y[0]=B[0]
    for i in range(1,Matrix_row_num):
        s=0
        for t in range(i):
            s=s+A[i][t]*y[t]
            G_num=G_num+1
        y[i]=B[i]-s
    x[Matrix_row_num-1]=round(y[Matrix_row_num-1]/A[Matrix_row_num-1][Matrix_row_num-1],3)
    for i in range(Matrix_row_num-1):
        n=Matrix_row_num-2-i
        s=0
        for t in range(n+1,Matrix_row_num):
            s=s+A[n][t]*x[t]
            G_num=G_num+1
        x[n]=round((y[n]-s)/A[n][n],3)   #保留小数点后三位
    return [list(A),time.clock()-G_time,G_num,x]
```

### 3、Crout消去法

##### 3.1 算法

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/numerical_analysis/crout.JPG)

##### 3.2 Crout消去法算法的程序实现

```python
def Crout(Matrix,Matrix_row_num,Matrix_col_num,B):
    G_num=0
    G_time=time.clock()
    A=Matrix
    for k in range(Matrix_row_num):
        for i in range(k,Matrix_row_num):
            s=0
            for t in range(k):
                s=s+A[i][t]*A[t][k]
                G_num=G_num+1
            A[i][k]=Matrix[i][k]-s
        for j in range(k+1,Matrix_row_num):
            if k<Matrix_row_num-1:
                s=0
                for t in range(k):
                    s=s+A[k][t]*A[t][j]
                    G_num=G_num+1
                A[k][j]=(Matrix[k][j]-s)/A[k][k]
    y=[i for i in range(Matrix_row_num)]
    x=[i for i in range(Matrix_row_num)]
    y[0]=B[0]/A[0][0]
    for i in range(1,Matrix_row_num):
        s=0
        for t in range(i):
            s=s+A[i][t]*y[t]
            G_num=G_num+1
        y[i]=(B[i]-s)/A[i][i]
    x[Matrix_row_num-1]=round(y[Matrix_row_num-1],3)
    for i in range(Matrix_row_num-1):
        n=Matrix_row_num-2-i
        s=0
        for t in range(n+1,Matrix_row_num):
            s=s+A[n][t]*x[t]
            G_num=G_num+1
        x[n]=round(y[n]-s,3)   #保留小数点后三位
    return [list(A),time.clock()-G_time,G_num,x]
```



### 4、GUI界面设计

为了便于对比和方便使用，建立了GUI界面

##### 4.1 代码

```python
# -*- coding: utf-8 -*-

# Form implementation generated from reading ui file 'Linear.ui'
#
# Created by: PyQt5 UI code generator 5.6
#
# WARNING! All changes made in this file will be lost!

from PyQt5 import QtCore, QtGui, QtWidgets

import sys,numpy,time

def Gauss(Matrix,Matrix_row_num,Matrix_col_num,B):
    G_num=0
    G_time=time.clock()
    A=Matrix
    for k in range(Matrix_row_num-1):
        Max_i_list=[]
        for i in range(k,Matrix_row_num):
            G_num=G_num+1
            Max_i_list.append(A[i][k])
        Max_i=max(Max_i_list)
        Max_i_index=Max_i_list.index(Max_i)+k
        M_t=A[Max_i_index]+0
        A[Max_i_index]=A[k]
        A[k]=M_t
        B_t=B[Max_i_index]
        B[Max_i_index]=B[k]
        B[k]=B_t
        for ii in range(k+1,Matrix_row_num):
            m_ik=A[ii][k]/A[k][k]
            for jj in range(k+1,Matrix_col_num):
                A[ii][jj]=A[ii][jj]-m_ik*A[k][jj]
                G_num=G_num+1
            A[ii][k]=0
            B[ii]=B[ii]-m_ik*B[k]

    '''回带过程'''
    x=[i for i in range(Matrix_row_num)]
    x[Matrix_row_num-1]=B[Matrix_row_num-1]/A[Matrix_row_num-1][Matrix_row_num-1]  #保留小数点后三位
    x[Matrix_row_num-1]=round(x[Matrix_row_num-1],3)
    for k in range(Matrix_row_num-1):
        n=Matrix_row_num-2-k
        s=0
        for j in range(n+1,Matrix_row_num):
            s=s+A[n][j]*x[j]
            G_num=G_num+1
        x[n]=round((B[n]-s)/A[n][n],3)   #保留小数点后三位
    return [list(A),time.clock()-G_time,G_num,x]

def Doolittle(Matrix,Matrix_row_num,Matrix_col_num,B):
    G_num=0
    G_time=time.clock()
    A=Matrix
    for k in range(Matrix_row_num):
        for j in range(k,Matrix_row_num):
            s=0
            for t in range(k):
                s=s+A[k][t]*A[t][j]
                G_num=G_num+1
            A[k][j]=Matrix[k][j]-s
        for i in range(k+1,Matrix_row_num):
            if k<Matrix_row_num:
                s=0
                for t in range(k):
                    s=s+A[i][t]*A[t][k]
                    G_num=G_num+1
                A[i][k]=(Matrix[i][k]-s)/A[k][k]
    y=[i for i in range(Matrix_row_num)]
    x=[i for i in range(Matrix_row_num)]
    y[0]=B[0]
    for i in range(1,Matrix_row_num):
        s=0
        for t in range(i):
            s=s+A[i][t]*y[t]
            G_num=G_num+1
        y[i]=B[i]-s
    x[Matrix_row_num-1]=round(y[Matrix_row_num-1]/A[Matrix_row_num-1][Matrix_row_num-1],3)
    for i in range(Matrix_row_num-1):
        n=Matrix_row_num-2-i
        s=0
        for t in range(n+1,Matrix_row_num):
            s=s+A[n][t]*x[t]
            G_num=G_num+1
        x[n]=round((y[n]-s)/A[n][n],3)   #保留小数点后三位
    return [list(A),time.clock()-G_time,G_num,x]
    
    
def Crout(Matrix,Matrix_row_num,Matrix_col_num,B):
    G_num=0
    G_time=time.clock()
    A=Matrix
    for k in range(Matrix_row_num):
        for i in range(k,Matrix_row_num):
            s=0
            for t in range(k):
                s=s+A[i][t]*A[t][k]
                G_num=G_num+1
            A[i][k]=Matrix[i][k]-s
        for j in range(k+1,Matrix_row_num):
            if k<Matrix_row_num-1:
                s=0
                for t in range(k):
                    s=s+A[k][t]*A[t][j]
                    G_num=G_num+1
                A[k][j]=(Matrix[k][j]-s)/A[k][k]
    y=[i for i in range(Matrix_row_num)]
    x=[i for i in range(Matrix_row_num)]
    y[0]=B[0]/A[0][0]
    for i in range(1,Matrix_row_num):
        s=0
        for t in range(i):
            s=s+A[i][t]*y[t]
            G_num=G_num+1
        y[i]=(B[i]-s)/A[i][i]
    x[Matrix_row_num-1]=round(y[Matrix_row_num-1],3)
    for i in range(Matrix_row_num-1):
        n=Matrix_row_num-2-i
        s=0
        for t in range(n+1,Matrix_row_num):
            s=s+A[n][t]*x[t]
            G_num=G_num+1
        x[n]=round(y[n]-s,3)   #保留小数点后三位
    return [list(A),time.clock()-G_time,G_num,x]

class Ui_Linear_Equation(object):
    def setupUi(self, Linear_Equation):
        Linear_Equation.setObjectName("Linear_Equation")
        Linear_Equation.resize(526, 683)
        font = QtGui.QFont()
        font.setFamily("Adobe Devanagari")
        font.setBold(True)
        font.setWeight(75)
        Linear_Equation.setFont(font)
        self.radioButton = QtWidgets.QRadioButton(Linear_Equation)
        self.radioButton.setGeometry(QtCore.QRect(70, 280, 131, 16))
        self.radioButton.setObjectName("radioButton")
        self.radioButton_2 = QtWidgets.QRadioButton(Linear_Equation)
        self.radioButton_2.setGeometry(QtCore.QRect(240, 280, 111, 16))
        self.radioButton_2.setObjectName("radioButton_2")
        self.radioButton_3 = QtWidgets.QRadioButton(Linear_Equation)
        self.radioButton_3.setGeometry(QtCore.QRect(380, 280, 89, 16))
        self.radioButton_3.setObjectName("radioButton_3")
        self.textEdit = QtWidgets.QTextEdit(Linear_Equation)
        self.textEdit.setGeometry(QtCore.QRect(150, 120, 351, 81))
        self.textEdit.setObjectName("textEdit")
        self.label = QtWidgets.QLabel(Linear_Equation)
        self.label.setGeometry(QtCore.QRect(140, 10, 381, 51))
        font = QtGui.QFont()
        font.setFamily("Adobe Devanagari")
        font.setPointSize(20)
        font.setBold(True)
        font.setWeight(75)
        self.label.setFont(font)
        self.label.setObjectName("label")
        self.label_2 = QtWidgets.QLabel(Linear_Equation)
        self.label_2.setGeometry(QtCore.QRect(40, 130, 91, 51))
        self.label_2.setObjectName("label_2")
        self.label_3 = QtWidgets.QLabel(Linear_Equation)
        self.label_3.setGeometry(QtCore.QRect(40, 220, 91, 51))
        self.label_3.setObjectName("label_3")
        self.lineEdit = QtWidgets.QLineEdit(Linear_Equation)
        self.lineEdit.setGeometry(QtCore.QRect(150, 230, 351, 20))
        self.lineEdit.setObjectName("lineEdit")
        self.label_4 = QtWidgets.QLabel(Linear_Equation)
        self.label_4.setGeometry(QtCore.QRect(360, 70, 101, 16))
        self.label_4.setObjectName("label_4")
        self.label_5 = QtWidgets.QLabel(Linear_Equation)
        self.label_5.setGeometry(QtCore.QRect(60, 380, 61, 20))
        self.label_5.setObjectName("label_5")
        self.lineEdit_2 = QtWidgets.QLineEdit(Linear_Equation)
        self.lineEdit_2.setGeometry(QtCore.QRect(120, 380, 61, 20))
        self.lineEdit_2.setObjectName("lineEdit_2")
        self.label_6 = QtWidgets.QLabel(Linear_Equation)
        self.label_6.setGeometry(QtCore.QRect(190, 380, 31, 16))
        self.label_6.setObjectName("label_6")
        self.lineEdit_3 = QtWidgets.QLineEdit(Linear_Equation)
        self.lineEdit_3.setGeometry(QtCore.QRect(360, 380, 61, 20))
        self.lineEdit_3.setObjectName("lineEdit_3")
        self.label_7 = QtWidgets.QLabel(Linear_Equation)
        self.label_7.setGeometry(QtCore.QRect(430, 380, 31, 16))
        self.label_7.setObjectName("label_7")
        self.label_8 = QtWidgets.QLabel(Linear_Equation)
        self.label_8.setGeometry(QtCore.QRect(300, 380, 61, 20))
        self.label_8.setObjectName("label_8")
        self.label_9 = QtWidgets.QLabel(Linear_Equation)
        self.label_9.setGeometry(QtCore.QRect(40, 430, 61, 21))
        self.label_9.setObjectName("label_9")
        self.lineEdit_4 = QtWidgets.QLineEdit(Linear_Equation)
        self.lineEdit_4.setGeometry(QtCore.QRect(120, 430, 381, 20))
        self.lineEdit_4.setObjectName("lineEdit_4")
        self.label_10 = QtWidgets.QLabel(Linear_Equation)
        self.label_10.setGeometry(QtCore.QRect(40, 470, 91, 31))
        font = QtGui.QFont()
        font.setPointSize(14)
        self.label_10.setFont(font)
        self.label_10.setObjectName("label_10")
        self.textEdit_2 = QtWidgets.QTextEdit(Linear_Equation)
        self.textEdit_2.setGeometry(QtCore.QRect(40, 500, 461, 161))
        self.textEdit_2.setObjectName("textEdit_2")
        self.pushButton = QtWidgets.QPushButton(Linear_Equation)
        self.pushButton.setGeometry(QtCore.QRect(110, 320, 81, 31))
        font = QtGui.QFont()
        font.setFamily("Adobe Devanagari")
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.pushButton.setFont(font)
        self.pushButton.setObjectName("pushButton")
        self.pushButton_2 = QtWidgets.QPushButton(Linear_Equation)
        self.pushButton_2.setGeometry(QtCore.QRect(320, 320, 81, 31))
        font = QtGui.QFont()
        font.setFamily("Adobe Devanagari")
        font.setPointSize(12)
        font.setBold(True)
        font.setWeight(75)
        self.pushButton_2.setFont(font)
        self.pushButton_2.setObjectName("pushButton_2")

        self.retranslateUi(Linear_Equation)
        self.pushButton.clicked.connect(self.calculate)
        self.pushButton_2.clicked.connect(self.delete)
        QtCore.QMetaObject.connectSlotsByName(Linear_Equation)
        

    def retranslateUi(self, Linear_Equation):
        _translate = QtCore.QCoreApplication.translate
        Linear_Equation.setWindowTitle(_translate("Linear_Equation", "Form"))
        self.radioButton.setText(_translate("Linear_Equation", "列主元Gauss消去法"))
        self.radioButton_2.setText(_translate("Linear_Equation", "Doolittle分解法"))
        self.radioButton_3.setText(_translate("Linear_Equation", "Crout分解法"))
        self.label.setText(_translate("Linear_Equation", "线性方程组求解器"))
        self.label_2.setText(_translate("Linear_Equation", "请输入系数矩阵"))
        self.label_3.setText(_translate("Linear_Equation", "请输入b向量"))
        self.label_4.setText(_translate("Linear_Equation", "制作人：张凡"))
        self.label_5.setText(_translate("Linear_Equation", "计算步数"))
        self.label_6.setText(_translate("Linear_Equation", "步"))
        self.label_7.setText(_translate("Linear_Equation", "毫秒"))
        self.label_8.setText(_translate("Linear_Equation", "计算用时"))
        self.label_9.setText(_translate("Linear_Equation", "解向量x"))
        self.label_10.setText(_translate("Linear_Equation", "其它信息"))
        self.pushButton.setText(_translate("Linear_Equation", "计算"))
        self.pushButton_2.setText(_translate("Linear_Equation", "清空输入"))
        
    def calculate(self):
        if self.lineEdit.text() and self.textEdit.toPlainText():
            Matrix_input=str(self.textEdit.toPlainText())
            B_input=str(self.lineEdit.text())
            B_v=B_input.split(',')
            B=[]
            for b in B_v:
                B.append(float(b))
            Matrix_row=Matrix_input.split(';')
            Matrix_row_num=len(Matrix_row)
            Matrix_col_num=len(Matrix_row[0].split(','))
            M=[]
            for i in Matrix_row:
                M0=i.split(',')
                M1=[]
                for j in M0:
                    M1.append(float(j))
                M.append(M1)
            Matrix=numpy.array(M)
            te='列主元Gauss消元前的矩阵：\n'
            for i in range(Matrix_row_num):
                t=''
                for j in range(Matrix_col_num):
                    t=t+str(round(Matrix[i][j],3))+'   '
                te=te+t+'\n'
            if self.radioButton.isChecked():
                result=Gauss(Matrix,Matrix_row_num,Matrix_col_num,B)
                self.lineEdit_2.clear()
                self.lineEdit_2.insert(str(result[2]))
                self.lineEdit_3.clear()
                self.lineEdit_3.insert(str(round(result[1],6)*1000))
                self.lineEdit_4.clear()
                self.lineEdit_4.insert(str(result[3]))
                self.textEdit_2.clear()
                te=te+'列主元Gauss消元后的矩阵：\n'
                for i in range(Matrix_row_num):
                    t=''
                    for j in range(Matrix_col_num):
                        t=t+str(round(result[0][i][j],3))+'   '
                    te=te+t+'\n'
                self.textEdit_2.setText(te)
            elif self.radioButton_2.isChecked():
                result=Doolittle(Matrix,Matrix_row_num,Matrix_col_num,B)
                self.lineEdit_2.clear()
                self.lineEdit_2.insert(str(result[2]))
                self.lineEdit_3.clear()
                self.lineEdit_3.insert(str(round(result[1],6)*1000))
                self.lineEdit_4.clear()
                self.lineEdit_4.insert(str(result[3]))
                self.textEdit_2.clear()
                te=te+'Doolittle消元后的矩阵：\n'
                for i in range(Matrix_row_num):
                    t=''
                    for j in range(Matrix_col_num):
                        t=t+str(round(result[0][i][j],3))+'   '
                    te=te+t+'\n'
                self.textEdit_2.setText(te)
            elif self.radioButton_3.isChecked():
                result=Crout(Matrix,Matrix_row_num,Matrix_col_num,B)
                self.lineEdit_2.clear()
                self.lineEdit_2.insert(str(result[2]))
                self.lineEdit_3.clear()
                self.lineEdit_3.insert(str(round(result[1],6)*1000))
                self.lineEdit_4.clear()
                self.lineEdit_4.insert(str(result[3]))
                self.textEdit_2.clear()
                te=te+'Crout消元后的矩阵：\n'
                for i in range(Matrix_row_num):
                    t=''
                    for j in range(Matrix_col_num):
                        t=t+str(round(result[0][i][j],3))+'   '
                    te=te+t+'\n'
                self.textEdit_2.setText(te)
        else :
            pass
        print(self.radiobutton.isChecked(),self.radiobutton_2.isChecked(),self.radiobutton_3.isChecked())
    def delete(self):
        self.lineEdit.clear()
        self.lineEdit_2.clear()
        self.lineEdit_3.clear()
        self.lineEdit_4.clear()
        self.textEdit.clear()
        self.textEdit_2.clear()
        

if __name__ == "__main__":
    app = QtWidgets.QApplication(sys.argv)
    MainWindow = QtWidgets.QMainWindow()
    ui = Ui_Linear_Equation()
    ui.setupUi(MainWindow)
    MainWindow.show()
    sys.exit(app.exec_())
```

##### 4.2 GUI预览

![](https://aerozf.oss-cn-beijing.aliyuncs.com/images/numerical_analysis/xianxingfangchengqiujie.gif)
