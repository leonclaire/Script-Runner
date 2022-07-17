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

Sample code:

    #pragma comment(lib,"F:\\Public\\sr.lib")

    int main()
    {
        SetScriptDir("XXX");  //脚本目录
        SetToolDir("XXX");    //工具目录
        SetLogPath("XXX");  //日志路径

        SetRegPath("XXX");  //注册表路径

        ClearScript();  //卸载脚本
        if (!LoadScript(g_path, &g_text))  //加载脚本
        {
            return FALSE;
        }

        ShowScript();  //打印脚本
        CloseScript(&g_text);  //关闭脚本

        ClearProcess(g_node);  //删除进度
        LoadProcess(g_node);  //加载进度
        SaveProcess(g_node);  //保存进度
        StopProcess();  //停止流程

        while (HaveProcess())  //流程没完成
        {
            if (!g_running)
            {
                goto EXIT;
            }

            GetLinePos(start, end);  //获取当前cmd文本位置
            status = ExecuteProcess();  //继续流程
        }

        return 0;
    }
