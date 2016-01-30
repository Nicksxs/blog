title: MFC 模态对话框
date: 2014-12-24 09:35:37
categories: C++
tags: [c++, mfc]
---
``` C++
void CTestDialog::OnBnClickedOk() 
{
	CString m_SrcTest;
	int nIndex = m_CbTest.GetCurSel(); 
	m_CbTest.GetLBText(nIndex, m_SrcTest);  
	OnOK();
}
```

模态对话框弹出确定后，在弹出对话框时新建的类及其变量会存在，但是对于其中的控件  
对象无法调用函数，即如果要在主对话框中获得弹出对话框的Combo box选中值的话，需  
要在弹出  对话框的确定函数内将其值取出，赋值给弹出对话框的公有变量，这样就可以  
在主对话框类得到值。  
  
