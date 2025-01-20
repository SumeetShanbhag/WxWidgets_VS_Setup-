# Setting up wxWidgets in Visual Studio

This guide shows you how to set up wxWidgets in Visual Studio step by step.

---

## 1. Download and Extract

1. Go to [wxwidgets.org/downloads](https://www.wxwidgets.org/downloads).  
2. Download the ZIP from **Source Code**.  
3. Extract the contents to a convenient location (e.g., `C:/Users/Username/Documents`).

---

## 2. Set the WXWIN Environment Variable

4. Open **System Environment Variables** from the Windows Start Menu.  
5. Go to `System Properties` → `Advanced` → `Environment Variables`.  
6. Under **System variables**, click **New**:  
   - **Variable name**: `WXWIN`  
   - **Variable value**: Path to the extracted folder (e.g., `C:\Users\Sumeet\Documents\wxWidgets-3.2.6`).  
7. Click **OK** on all dialog boxes to confirm and close.

---

## 3. Build wxWidgets

8. Go to the `msw` folder in the extracted directory (e.g., `C:\Users\Sumeet\Documents\wxWidgets-3.2.6\build\msw`).  
9. Open the solution file (`wx_vc16.sln` or `wx_vc17.sln`) in Visual Studio.  
10. Set configuration to **Debug**, platform to **Win32**, then go to **Build** → **Build Solution**.  
11. Repeat the build process for:
    - **Release**, **Win32**
    - **Debug**, **x64**
    - **Release**, **x64**
12. When complete, two new folders will appear:
    - `C:\Users\Sumeet\Documents\wxWidgets-3.2.6\lib\vc_lib`
    - `C:\Users\Sumeet\Documents\wxWidgets-3.2.6\lib\vc_x64_lib`

---

## 4. Create a Test Project

13. In Visual Studio, create an **Empty Project** (ensure you add a `.cpp` file).  
14. Insert the following code in your `.cpp` file (indented below):

    ```cpp
    #include <wx/wx.h>
    
    class App : public wxApp {
    public:
        bool OnInit() {
            wxFrame* window = new wxFrame(NULL, wxID_ANY, "GUI Test", 
                                          wxDefaultPosition, wxSize(600, 400));
            wxBoxSizer* sizer = new wxBoxSizer(wxHORIZONTAL);
            wxStaticText* text = new wxStaticText(window, wxID_ANY, 
                                                  "Well Done!\nEverything seems to be working",
                                                  wxDefaultPosition, wxDefaultSize, 
                                                  wxALIGN_CENTRE_HORIZONTAL);
            text->SetFont(wxFont(20, wxFONTFAMILY_DEFAULT, 
                                 wxFONTSTYLE_NORMAL, wxFONTWEIGHT_NORMAL));
            sizer->Add(text, 1, wxALIGN_CENTER);
            window->SetSizer(sizer);
            window->Show();
            return true;
        }
    };
    
    wxIMPLEMENT_APP(App);
    ```

---

## 5. Configure Project Properties

15. Right-click your project → **Properties**.  
16. Ensure **Configuration** = *All Configurations*, and **Platform** = *All Platforms*.

### C/C++ → Additional Include Directories

17. Under **Configuration Properties** → **C/C++** → **Additional Include Directories**, click **Edit**.  
18. Add:
    ```
    $(WXWIN)\include
    $(WXWIN)\include\msvc
    ```
19. Press **OK**, then **Apply**.

### Linker → System

20. Go to **Linker** → **System** → **Subsystem** and change it from **Console** to **Windows**. Click **Apply**.

### Linker → General → Additional Library Directories

21. Set **Platform** to **Win32**, then go to **Linker** → **General** → **Additional Library Directories**.  
    - Add:
      ```
      $(WXWIN)\lib\vc_lib
      ```
    - Click **Apply**.

22. Set **Platform** to **x64**, then again go to **Linker** → **General** → **Additional Library Directories**.  
    - Add:
      ```
      $(WXWIN)\lib\vc_x64_lib
      ```
    - Click **Apply**.

---

## 6. Run the Program

23. **Now the environment is set up.** The code should compile and run in both **Debug** and **Release** modes for **Win32** and **x64**. Simply build and run the project to see your `wxWidgets` test window.
