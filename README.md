# SWIFT UITextView 实现 placeHolder

## 实现原理
### 备注：方法比较笨，但是可以解决基本需求
### 1、构造一个UITextView,默认填充自己需要的placeholder,并且设置颜色为灰色
### 2、监听UITextView的三个事件来改变字体颜色和文字内容：textViewDidBeginEditing ， textViewShouldEndEditing ， textViewDidChange 。

### 代码：
	 //存放编辑过的内容
	 var userContent: String! = ""

    @IBOutlet weak var contentTv: UITextView!

    override func viewDidLoad() {
        super.viewDidLoad()
        //默认构造的UITextView
        contentTv.layer.borderWidth = 1;
        contentTv.font = UIFont.boldSystemFont(ofSize: 16)
        contentTv.layer.borderColor = UIColor.lightGray.cgColor
        contentTv.layer.cornerRadius = 5
        }

    //获取焦点时候调用
    func textViewDidBeginEditing(_ textView: UITextView) {
        textView.textColor = UIColor.black
          var size = userContent?.characters.count
        if size! <= 0 {
           textView.text=""
        }
    }

    //编辑结束，离开textView时调用
    func textViewShouldEndEditing(_ textView: UITextView) -> Bool {
       var size = userContent?.characters.count
        if size! <= 0 {
           textView.textColor =  UIColor.lightGray
           textView.text = "Leave your suggestions, bug reports or new feature requirements here. Let's work together to make better."
        }//这里必须返回true，false的话点击别的控件焦点不会离开当前的textview
        return true
    }

    //tv中的文字发生改变时会调用
    func textViewDidChange(_ textView: UITextView) {
        let index:Int = textView.text.characters.count
         var string =  textView.text
          textView.textColor = UIColor.black
        userContent = string        
    }
