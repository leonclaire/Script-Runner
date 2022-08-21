The easiest way to run command script.

Attention:

    no trojan, no backdoor...

Interface:

    VOID  GetLinePos(UINT64&, UINT64&);
    VOID  SetToolDir(PCSTR);
    VOID  SetScriptDir(PCSTR);
    VOID  SetLogPath(PCSTR);
    VOID  SetRegPath(PCSTR);

    BOOL LoadScript(PCSTR, PSTR*);
    VOID  CloseScript(PSTR*);
    VOID  ClearScript();

    VOID  ClearProcess(PCSTR);
    VOID  LoadProcess(PCSTR);
    VOID  SaveProcess(PCSTR);
    VOID  StopProcess();
    BOOL  HaveProcess();
    DWORD  ExecuteProcess();
    VOID GoNextStep();    

Sample code:

    #pragma comment(lib,"F:\\Public\\sr.lib")

    int main()
    {
        SetScriptDir("XXX");   //脚本目录
        SetToolDir("XXX");     //工具目录
        SetLogPath("XXX");     //日志路径

        SetRegPath("XXX");     //注册表路径

        ClearScript();         //卸载脚本
        if (!LoadScript("XXX", &text)) //加载脚本
        {
            return 1;
        }

        ShowScript();          //打印脚本
        CloseScript(&text);    //关闭脚本

        ClearProcess("XXX");   //删除进度
        LoadProcess("XXX");    //加载进度
        SaveProcess("XXX");    //保存进度
        StopProcess();         //停止流程

        while (HaveProcess())  //流程没完成
        {
            GetLinePos(start, end);     //获取当前cmd在text位置
            status = ExecuteProcess();  //执行流程
            GoNextStep();            
        }

        return 0;
    }
