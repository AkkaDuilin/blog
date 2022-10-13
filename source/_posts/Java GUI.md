---
title: Java GUI
categories:
  - Java

  - null
tags:
  - Java
  - GUI
copyright: true
date: 2022-04-02 09:29:22
permalink:
description:
image:
---

<img src="https://" alt="" style="width:100%" />  

**前言**

Swing 是一个为Java设计的GUI工具包。

Swing是JAVA基础类的一部分。

Swing包括了图形用户界面（GUI）器件如：文本框，按钮，分隔窗格和表。

http://c.biancheng.net/view/1209.html

<!-- more -->

# JFrame

JFrame 用来设计类似于 Windows 系统中窗口形式的界面。JFrame 是 Swing 组件的顶层容器，该类继承了 AWT 的 Frame 类，支持 Swing 体系结构的高级 GUI 属性。

<table border="1">
	<caption>
		表1 JFrame类的常用方法</caption>
	<tbody>
		<tr>
			<th>
				方法名称</th>
			<th>
				概述</th>
		</tr>
		<tr>
			<td>
				getContentPane()</td>
			<td>
				返回此窗体的 contentPane 对象</td>
		</tr>
		<tr>
			<td>
				getDefaultCloseOperation()</td>
			<td>
				返回用户在此窗体上单击&ldquo;关闭&rdquo;按钮时执行的操作</td>
		</tr>
		<tr>
			<td>
				setContentPane(Container contentPane)</td>
			<td>
				设置 contentPane 属性</td>
		</tr>
		<tr>
			<td>
				setDefaultCloseOperation(int operation)</td>
			<td>
				设置用户在此窗体上单击&ldquo;关闭&rdquo;按钮时默认执行的操作</td>
		</tr>
		<tr>
			<td>
				setDefaultLookAndFeelDecorated (boolean<br />
				defaultLookAndFeelDecorated)</td>
			<td>
				设置 JFrame 窗口使用的 Windows 外观（如边框、关<br />
				闭窗口的 小部件、标题等）</td>
		</tr>
		<tr>
			<td>
				setIconImage(Image image)</td>
			<td>
				设置要作为此窗口图标显不的图像</td>
		</tr>
		<tr>
			<td>
				setJMenuBar( JMenuBar menubar)</td>
			<td>
				设置此窗体的菜单栏</td>
		</tr>
		<tr>
			<td>
				setLayout(LayoutManager manager)</td>
			<td>
				设置&nbsp;LayoutManager&nbsp;属性</td>
		</tr>
		<tr>
			<td>
				setDefaultCloseOperation(JDialog.DISPOSE_ON_CLOSE);</td>
			<td>
				设置用户在此窗体上发起 "close" 时默认执行的操作。必须指定以下选项之一：DO_NOTHING_ON_CLOSE（在 WindowConstants 中定义）：不执行任何操作；要求程序在已注册的WindowListener 对象的 windowClosing 方法中处理该操作。
				HIDE_ON_CLOSE（在 WindowConstants 中定义）：调用任意已注册的 WindowListener 对象后自动隐藏该窗体。
				DISPOSE_ON_CLOSE（在 WindowConstants 中定义）：调用任意已注册 WindowListener 的对象后自动隐藏并释放该窗体。
				EXIT_ON_CLOSE（在 JFrame 中定义）：使用 System exit 方法退出应用程序。仅在应用程序中使用。
			</td>
		</tr>
	</tbody>
</table>

# JPanel

JPanel 是一种中间层容器，它能容纳组件并将组件组合在一起，但它本身必须添加到其他容器中使用。JPanel 类的构造方法如下。
1. JPanel()：使用默认的布局管理器创建新面板，默认的布局管理器为 FlowLayout。
2. JPanel(LayoutManagerLayout layout)：创建指定布局管理器的 JPanel 对象。

<table border="1">
	<caption>
		表2 JPanel类的常用方法</caption>
	<tbody>
		<tr>
			<th>
				方法名及返回值类型</th>
			<th>
				说明</th>
		</tr>
		<tr>
			<td>
				Component add(Component comp)</td>
			<td>
				将指定的组件追加到此容器的尾部</td>
		</tr>
		<tr>
			<td>
				void remove(Component comp)</td>
			<td>
				从容器中移除指定的组件</td>
		</tr>
		<tr>
			<td>
				void setFont(Font f)</td>
			<td>
				设置容器的字体</td>
		</tr>
		<tr>
			<td>
				void setLayout(LayoutManager mgr)</td>
			<td>
				设置容器的布局管理器</td>
		</tr>
		<tr>
			<td>
				void setBackground(Color c)</td>
			<td>
				设置组件的背景色</td>
		</tr>
	</tbody>
</table>wdas
# xx3x


# 布局管理器

## BorderLayout 边框布局管理器
边框布局管理器将窗口分为 5 个区域：North、South、East、West 和 Center。
BorderLayout 布局管理器的构造方法如下所示。
BorderLayout()：创建一个 Border 布局，组件之间没有间隙。
BorderLayout(int hgap,int vgap)：创建一个 Border 布局，其中 hgap 表示组件之间的横向间隔；vgap 表示组件之间的纵向间隔，单位是像素。

## FlowLayout   流式布局管理器
FlowLayout 布局管理器不限制它所管理组件的大小，而是允许它们有自己的最佳大小。
FlowLayout 布局管理器的构造方法如下。
FlowLayout()：创建一个布局管理器，使用默认的居中对齐方式和默认 5 像素的水平和垂直间隔。
FlowLayout(int align)：创建一个布局管理器，使用默认 5 像素的水平和垂直间隔。其中，align 表示组件的对齐方式，对齐的值必须是 FlowLayoutLEFT、FlowLayout.RIGHT 和 FlowLayout.CENTER，指定组件在这一行的位置是居左对齐、居右对齐或居中对齐。
FlowLayout(int align, int hgap,int vgap)：创建一个布局管理器，其中 align 表示组件的对齐方式；hgap 表示组件之间的横向间隔；vgap 表示组件之间的纵向间隔，单位是像素。

## CardLayout 卡片布局管理器
CardLayout 布局管理器将容器分成许多层，每层的显示空间占据整个容器的大小，但是每层只允许放置一个组件。CardLayout 的构造方法如下。
CardLayout()：构造一个新布局，默认间隔为 0。
CardLayout(int hgap, int vgap)：创建布局管理器，并指定组件间的水平间隔（hgap）和垂直间隔（vgap）。


## GridLayout 网格布局管理器
GridLayout 布局管理器将组件分布在一个网格中，每个网格占据一个容器的尺寸。
GridLayout 的构造方法如下。
GridLayout()：创建一个新的网格布局，默认的行数为 1，默认的列数为 1，默认的水平间隔为 5 像素，默认的垂直间隔为 5 像素。
GridLayout(int rows, int cols,int hgap,int vgap)：创建一个新的网格布局，其中 rows 表示网格的行数，cols 表示网格的列数。并且可以指定组件之间横向（hgap）和纵向（vgap）的间隔，单位是像素。

## GridBagLayout 网格包布局管理器
GridBagLayout 布局管理器将组件分布在一个网格中，每个网格占据一个容器的尺寸。GridBagLayout 不需要组件的尺寸一致，允许组件扩展到多行多列。
GridBagLayout 的构造方法如下。
GridBagLayout()：创建一个新的网格包布局，默认的行数为 1，默认的列数为 1，默认的水平间隔为 5 像素，默认的垂直间隔为 5 像素。


##  BoxLayout 盒布局管理器
BoxLayout 布局管理器将组件分布在一个盒子中，盒子的大小由组件的大小决定。
BoxLayout 的构造方法如下。
BoxLayout(int axis)：创建一个新的盒布局，其中 axis 表示组件的布局方向，对齐的值必须是 BoxLayout.X_AXIS 或 BoxLayout.Y_AXIS。

<table border="1">
	<caption>
		表1 Box类设置组件间隔的静态方法</caption>
	<tbody>
		<tr>
			<th>
				网格包布局</th>
			<th>
				说明</th>
		</tr>
		<tr>
			<td>
				static Component createHorizontalGlue()</td>
			<td>
				创建一个不可见的、可以被水平拉伸和收缩的组件</td>
		</tr>
		<tr>
			<td>
				static Component createVerticalGlue()</td>
			<td>
				创建一个不可见的、可以被垂直拉伸和收缩的组件</td>
		</tr>
		<tr>
			<td>
				static Component createHorizontalStrut(int width)</td>
			<td>
				创建一个不可见的、固定宽度的组件</td>
		</tr>
		<tr>
			<td>
				static Component createVerticalStrut(int height)</td>
			<td>
				创建一个不可见的、固定高度的组件</td>
		</tr>
		<tr>
			<td>
				static Component createRigidArea(Dimension d)</td>
			<td>
				创建一个不可见的、总是具有指定大小的组件</td>
		</tr>
	</tbody>
</table>


# 标签组件

JLabel()：创建无图像并且标题为空字符串的 JLabel。
JLabel(Icon image)：创建具有指定图像的 JLabel。
JLabel(String text)：创建具有指定文本的 JLabel。
JLabel(String textjcon image,int horizontalAlignment)：创建具有指定文本、图像和水平对齐方式的 JLabel，horizontalAlignment 的取值有 3 个，即 JLabel.LEFT、JLabel.RIGHT 和 JLabel.CENTER。

<table border="1">
	<caption>
		表1 JLabel类的常用方法</caption>
	<tbody>
		<tr>
			<th>
				方法名称</th>
			<th>
				说明</th>
		</tr>
		<tr>
			<td>
				void setText(Stxing text)</td>
			<td>
				定义 JLabel 将要显示的单行文本</td>
		</tr>
		<tr>
			<td>
				void setIcon(Icon image)</td>
			<td>
				定义 JLabel 将要显示的图标</td>
		</tr>
		<tr>
			<td>
				void setIconTextGap(int iconTextGap)</td>
			<td>
				如果 JLabel 同时显示图标和文本，则此属性定义它们之间的间隔</td>
		</tr>
		<tr>
			<td>
				void setHorizontalTextPosition(int textPosition)</td>
			<td>
				设置 JLabel 的文本相对其图像的水平位置</td>
		</tr>
		<tr>
			<td>
				void setHorizontalAlignment(int alignment)</td>
			<td>
				设置标签内容沿 X 轴的对齐方式</td>
		</tr>
		<tr>
			<td>
				int getText()</td>
			<td>
				返回 JLabel 所显示的文本字符串</td>
		</tr>
		<tr>
			<td>
				Icon getIcon()</td>
			<td>
				返回 JLabel 显示的图形图像</td>
		</tr>
		<tr>
			<td>
				Component getLabelFor()</td>
			<td>
				获得将 JLabel 添加到的组件</td>
		</tr>
		<tr>
			<td>
				int getIconTextGap()</td>
			<td>
				返回此标签中显示的文本和图标之间的间隔量</td>
		</tr>
		<tr>
			<td>
				int getHorizontalTextPosition()</td>
			<td>
				返回 JLabel 的文本相对其图像的水平位置</td>
		</tr>
		<tr>
			<td>
				int getHorizontalAlignment()</td>
			<td>
				返回 JLabel 沿 X 轴的对齐方式</td>
		</tr>
	</tbody>
</table>

# 按钮组件
JButton()：创建一个无标签文本、无图标的按钮。
JButton(Icon icon)：创建一个无标签文本、有图标的按钮。
JButton(String text)：创建一个有标签文本、无图标的按钮。
JButton(String text,Icon icon)：创建一个有标签文本、有图标的按钮。

http://c.biancheng.net/view/1217.html

#  单行文本框组件
JTextField()：创建一个默认的文本框。
JTextField(String text)：创建一个指定初始化文本信息的文本框。
JTextField(int columns)：创建一个指定列数的文本框。
JTextField(String text,int columns)：创建一个既指定初始化文本信息，又指定列数的文本框。

# 文本域组件
文本域与文本框的最大区别就是文本域允许用户输入多行文本信息。
JTextArea()：创建一个默认的文本域。
JTextArea(int rows,int columns)：创建一个具有指定行数和列数的文本域。
JTextArea(String text)：创建一个包含指定文本的文本域。
JTextArea(String text,int rows,int columns)：创建一个既包含指定文本，又包含指定行数和列数的多行文本域。

# 选框组件
JCheckBox()：创建一个默认的复选框，在默认情况下既未指定文本，也未指定图像，并且未被选择。
JCheckBox(String text)：创建一个指定文本的复选框。
JCheckBox(String text,boolean selected)：创建一个指定文本和选择状态的复选框。

**JRadioButton 通常位于一个 ButtonGroup 按钮组中，不在按钮组中的 JRadioButton 也就失去了单选按钮的意义。**
使用时先创建一个ButtonGroup实例，再将创建的JRadioButton加入到ButtonGroup中，这样就可以实现单选按钮的功能。

JRadioButton()：创建一个初始化为未选择的单选按钮，其文本未设定。
JRadioButton(Icon icon)：创建一个初始化为未选择的单选按钮，其具有指定的图像但无文本。
JRadioButton(Icon icon,boolean selected)：创建一个具有指定图像和选择状态的单选按钮，但无文本。
JRadioButton(String text)：创建一个具有指定文本但未选择的单选按钮。
JRadioButton(String text,boolean selected)：创建一个具有指定文本和选择状态的单选按钮。
JRadioButton(String text,Icon icon)：创建一个具有指定的文本和图像并初始化为未选择的单选按钮。
JRadioButton(String text,Icon icon,boolean selected)：创建一个具有指定的文本、图像和选择状态的单选按钮。

# 下拉列表组件
JComboBox()：创建一个空的 JComboBox 对象。
JComboBox(ComboBoxModel aModel)：创建一个 JComboBox，其选项取自现有的 ComboBoxModel。
JComboBox(Object[] items)：创建包含指定数组中元素的 JComboBox。

JComboBox 能够响应 ItemEvent 事件和 ActionEvent 事件，其中 ItemEvent 触发的时机是当下拉列表框中的所选项更改时，ActionEvent 触发的时机是当用户在 JComboBox 上直接输入选择项并回车时。要处理这两个事件，需要创建相应的事件类并实现 ItemListener 接口和 ActionListener 接口。

# 事件监听
事件处理者（监听器）通常是一个类，该类如果能够处理某种类型的事件，就必须实现与该事件类型相对的接口。

## ActionEvent 动作事件监听器

接口： ActionListener

方法
1. addActionListener() 添加监听

添加指定的动作侦听器，以接收发自此按钮的动作事件。当用户在此按钮上按下或释放鼠标时，发生动作事件。如果 l 为 null，则不抛出任何异常，也不执行任何动作。

{% codeblock %}

<<<<<<< HEAD
=======
``` java
>>>>>>> 710f4efc6c546c0f3d7e8ec9d05d24339b6239ba
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
public class FrameDemo
{
    //定义该图形中所需的组件的引用
    private Frame f;
    private Button bt;

    //方法
    FrameDemo()//构造方法
    {
        madeFrame();
    }

    public void madeFrame()
    {
        f = new Frame("My Frame");

        //对Frame进行基本设置。
        f.setBounds(300,100,600,500);//对框架的位置和大小进行设置
        f.setLayout(new FlowLayout(FlowLayout.CENTER,5,5));//设计布局

        bt = new Button("My Button");

        //将组件添加到Frame中
        f.add(bt);

        //加载一下窗体上的事件
        myEvent();

        //显示窗体
        f.setVisible(true);
    }

    private void myEvent()
    {
        f.addWindowListener(new WindowAdapter()//窗口监听
        {
            public void windowClosing(WindowEvent e)
            {
                System.out.println("窗体执行关闭！");
                System.exit(0);
            }
        });
        //让按钮具备关闭窗口的功能
        bt.addActionListener(new ActionListener()
        {
            public void actionPerformed(ActionEvent e)
            {
                 System.out.println("按钮执行关闭窗口的功能");
                 System.exit(0);
            }
        });
    }

    public static void main(String[] agrs)
    {
        new FrameDemo();
    }
}
<<<<<<< HEAD
=======
```
>>>>>>> 710f4efc6c546c0f3d7e8ec9d05d24339b6239ba

{% endcodeblock %}

2. removeActionListener() 删除监听

## FocusEvent 焦点事件监听器

接口： FocusListener

FocusEvent 接口定义了两个方法，分别为 focusGained() 方法和 focusLost() 方法，其中 focusGained() 方法是在组件获得焦点时执行，focusLost() 方法是在组件失去焦点时执行。

方法
1. addFocusListener() 添加监听
{% codeblock  %}
JTextField txtfield1 = new JTextField(20);
txtfield1.addFocusListener(new FocusListener()
	{
		@Override
		public void focusGained(FocusEvent arg0)
		{
			// 获取焦点时执行此方法
			label.setText("文本框获得焦点，正在输入内容");
		}
		@Override
		public void focusLost(FocusEvent arg0)
		{
			// 失去焦点时执行此方法
			label.setText("文本框失去焦点，内容输入完成");
		}
	});
{% endcodeblock %}

2. removeFocusListener() 删除监听

## ListSelectionEvent 选择事件监听器

列表框控件 JList 会显示很多项供用户选择，通常在使用时会根据用户选择的列表项完成不同的操作.

接口： ListSelectionListener

1. addListSelectionListener() 添加监听
{% codeblock %}
JList list = new JList(new String[]{"Java", "C++", "C#", "Python", "PHP", "JavaScript"});
list.addListSelectionListener(new ListSelectionListener()
{
	@Override
	public void valueChanged(ListSelectionEvent e)
	{
		// 当选择项发生变化时执行此方法
		label.setText("选择了" + list.getSelectedValue());
	}
});
{% endcodeblock %}

2. removeListSelectionListener() 删除监听


# JSlider

滑块（JSlider）是一个允许用户在有限区间内通过移动滑块来选择值的组件。

**JSlider(int min,int max,int value)**	
用指定的最小值、最大值和初始值创建一个水平滑块。

#  JProgressBar
进度条（JProgressBar）是一种以可视化形式显示某些任务进度的组件。JProgressBar 类实现了一个用于为长时间的操作提供可视化指示器的 GUI 进度条。在任务的完成进度中，进度条显示该任务完成的百分比。

ProgressBar 类的常用构造方法和 JSlider 类的常用构造方法一样

# Timer
计时器（Timer）组件可以在指定时间间隔触发一个或多个 ActionEvent。

第一个参数为事件触发之间的间隔 单位为毫秒
第二个参数为ActionListener

{% codeblock %}
Timer timer = new Timer(1000, new ActionListener()
{
	@Override
	public void actionPerformed(ActionEvent e)
	{
		// 每隔一秒执行一次
		label.setText("计时器触发了一次");
	}
});
timer.start();
{% endcodeblock %}

# JTable

JTable()：构造一个默认的 JTable，使用默认的数据模型、默认的列模型和默认的选择模型对其进行初始化。
JTable(int numRows,int numColumns)：使用 DefaultTableModel 构造具有 numRows 行和 numColumns 列个空单元格的 JTable。
JTable(Object[][] rowData,Object[] columnNames)：构造一个 JTable 来显示二 维数组 rowData 中的值，其列名称为 columnNames。

{% codeblock %}
JTable table = new JTable(new Object[][]{
		{"1", "2", "3", "4", "5"},
		{"6", "7", "8", "9", "10"}},
		new Object[]{"A", "B", "C", "D", "E"});
{% endcodeblock %}
		
# 其他组件

## JMenu
菜单由 Swing 中的 JMenu 类实现，可以包含多个菜单项和带分隔符的菜单。在菜单中，菜单项由 JMenuItem 类表示，分隔符由 JSeparator 类表示。

## 弹出式菜单 JPopuMenu
弹出式菜单由 JPopupMenu 类实现，它是一个可弹出并显示一系列选项的小窗口。它还用于当用户选择菜单项并激活它时显示的“右拉式(pull-right)”菜单，可以在想让菜单显示的任何其他位置使用。

## JToolBar 工具栏组件
工具栏提供了一个用来显示常用按钮和操作的组件

## JFileChooser 文件选择器
文件选择器为用户能够操作系统文件提供了桥梁。swing 中使用 JFileChooser 类实现文件选择器，该类常用的构造方法如下。
JFileChooser()：创建一个指向用户默认目录的 JFileChooser。
JFileChooser(File currentDirectory)：使用指定 File 作为路径来创建 JFileChooser。
JFileChooser(String currentDirectoryPath)：创建一个使用指定路径的 JFileChooser。
JFileChooser(String currentDirectoryPath, FileSystemView fsv)：使用指定的当前目录路径和 FileSystem View 构造一个 JFileChooser。

## JColorChooser 颜色选择器
JColorChooser()：创建初始颜色为白色的颜色选取器窗格。
JColorChooser(Color initialColor)：创建具有指定初始颜色的颜色选取器窗格。
JColorChooser(ColorSelectionModel model)：创建具有指定 ColorSelectionModel 颜色选取器窗格。

## JOptionPane
对话框通常用作从用户处接收附加信息，或者提供发生了某种事件的通知。Java 提供了 JOptionPane 类，用来创建标准对话框，也可以通过扩展 JDialog 类创建自定义的对话框。JOptionPane 类可以用来创建 4 种类型的标准对话框：确认对话框、消息对话框、输入对话框和选项对话框。

## JTabbedPane 选项卡组件
使用选项卡可以在有限的布局空间内展示更多的内容。Swing 使用 JTabbedPane 类实现选项卡。

JTabbedPane 类创建的选项卡可以通过单击标题或者图标在选项卡之间进行切换。JTabbedPane 类的常用构造方法如下所示。
JTabbedPane()：创建一个具有默认 JTabbedPane.TOP 布局的空 TabbedPane。
JTabbedPane(int tabPlacement)：创建一个空的 TabbedPane，使其具有以下指定选项卡布局中的一种：JTabbedPane.TOP、JTabbedPane.BOTTOM、JTabbedPane.LEFT 或 JTabbedPane.RIGHT。

<hr />         
版权信息