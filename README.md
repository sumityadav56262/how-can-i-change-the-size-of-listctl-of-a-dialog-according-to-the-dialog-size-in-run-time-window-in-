//how can i change the size of listctl of a dialog according to the dialog size in run time window in mfc by code
//To change the size of a list control on a dialog window according to the dialog size at runtime in MFC, you can handle the WM_SIZE message in your dialog class and //use the MoveWindow function to adjust the size of the list control.

//Here is an example of how to resize a list control on a dialog window in MFC based on the size of the dialog window:

//In your dialog class header file, add a member variable for the list control:
//c++
//Copy code

CListCtrl m_listControl;

//In the OnInitDialog function of your dialog class, create the list control and set its initial size:
//c++
//Copy code


BOOL CMyDialog::OnInitDialog()
{
    CDialogEx::OnInitDialog();

    // Create the list control
    m_listControl.Create(WS_VISIBLE | WS_CHILD | LVS_REPORT, CRect(0, 0, 0, 0), this, IDC_LIST_CONTROL);

    // Set the initial size of the list control
    CRect rect;
    GetClientRect(&rect);
    m_listControl.MoveWindow(rect.left, rect.top, rect.right - rect.left, rect.bottom - rect.top, TRUE);

    return TRUE;
}


//In the message map of your dialog class, add a handler for the WM_SIZE message:
//c++
//Copy code


BEGIN_MESSAGE_MAP(CMyDialog, CDialogEx)
    ON_WM_SIZE()
END_MESSAGE_MAP()


//In the implementation of the WM_SIZE handler, resize the list control based on the new size of the dialog window:
//c++
//Copy code


void CMyDialog::OnSize(UINT nType, int cx, int cy)
{
    CDialogEx::OnSize(nType, cx, cy);

    // Resize the list control
    m_listControl.MoveWindow(0, 0, cx, cy, TRUE);
}


//In this example, we first create the list control using the Create function, which sets the initial size of the control to (0,0). We then set the initial size of the //list control in the OnInitDialog function using the MoveWindow function. We get
