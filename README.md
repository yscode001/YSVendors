# YSVendor
基于常用三方库的二次封装
- MJRefresh
- SDWebImage

建议：使用时，把YSVendor下载下来，以本地库的方式进行使用和修改。

## RefreshControl：基于MJRefresh的刷新控件。

~~~swift
class ViewController: YSBaseVC {
    
    private lazy var tbv:UITableView = UITableView()
    
    // 创建刷新控件
    private lazy var refreshCtrl:YSRefreshCtrl = YSRefreshCtrl.ys.create(pulldown: {
        print("下拉刷新执行的闭包")
    }, pullup: {
        print("上拉加载执行的闭包")
    })
    
    override func viewDidLoad() {
        super.viewDidLoad()
        view.backgroundColor = .white
        
        // 把刷新控件设置给tableView，以下2种方式等价
        tbv.ys.setupRefreshCtrl(ctrl: refreshCtrl)
        refreshCtrl.ys.setupToTableView(tbv: tbv)
        
        // 自动刷新
        refreshCtrl.ys.autoPulldownRefresh()
        
        // 是否正在执行刷新和加载动作
        let _ = refreshCtrl.ys.isPulldownRefreshing
        let _ = refreshCtrl.ys.isPullupRefreshing
        
        // 结束刷新
        refreshCtrl.ys.endRefresh(pulldown: true, hasMore: true)

        // 设置标题数据
        refreshCtrl.ys.setupData(title: <#T##YSRefreshTitleInfo#>)
    }
}
~~~

## WebImage：基于SDWebImage，对UIImageView加载网络图片进行封装。

~~~swift
// 设置网络图片
UIImageView().ys.setImage(...)
~~~
