一、分类准则（共11个步骤）：
1) 若 χ2_star < χ2_gal & CS > 0.94 => star1
2) 若 χ2_star < χ2_qso & CS > 0.94 => star2
3) 定义非恒星样本no_star1 = all - (star1+star2).
4) 若 χ2_qso< χ2_gal & CS > 0.94: qso1
5) 若 χ2_qso< χ2_star & CS > 0.94: qso2
6) 定义准星系样本gal = no_star1-(qso1+qso2).
7) 定义星系样本gal_ext= gal & CS < 0.94
8) 把准星系样本里的点源部分，也就是gal_pl = gal & CS >0.94, 归类为恒星。
最后我们得到以下初步分类结果: 
Galaxy= gal_ext
Star= star1+ star2 + gal_pl 
QSO= no_star1 & （qso1+qso2）

在前面8个初步分类步骤的基础上，我们又增加了下面三个步骤，进一步提高分类的精确度：

9) mass_cut_star = (MASS_BEST < 7 & CLASS_STAR_i > 0.8) or MASS_BEST< 4.6 & 0.1 < CLASS_STAR_i < 0.8
10) mass_cut_qso = (MASS_BEST>7 & CLASS_STAR_i>0.8.5);
11) color_cut_stars = MAG_AUTO_g<18 [增加这个步骤是因为我们发现只使用前10个分类步骤的时候，qso的g - g-z的颜色图里MAG_AUTO_g<18有一群star的分布，故我们增加步骤11，把这群star划分回去给star]


二、工作步骤和程序说明：

1、	Lephare拟合输入：
/输入/BC03_CSST.para是lephare拟合的配置文件，/输入/data_lephare_z_v3是lephare拟合的输入数据，即CSST的多波段测光数据。/输入/CSST文件夹里是lephare拟合过程中需要使用到的CSST滤光片响应函数。

2、	Lephare拟合输出：
/输出/z_v3_slim.csv和/输出/z_free_slim.csv分别是固定和放开红移拟合的输出结果文件（其实是输入文件与输出文件的合并）。

3、	分类和结果：
/分类程序/separate_z_v3.py是对固定红移拟合结果“/输出/z_v3_slim.csv”，只使用分类准则前8个步骤的分类程序，分类完成得到参数type_xie，把它添加到原读写文件“/输出/z_v3_slim.csv”中，并另存为分类结果文件：/分类结果/z_v3.csv。
/分类程序/separate_z_v3_x.py是对固定红移拟合结果“/输出/z_v3_slim.csv”，使用分类准则完整11个步骤的分类程序，分类完成得到参数type_xie，把它添加到原读写文件“/输出/z_v3_slim.csv”中，并另存为分类结果文件：/分类结果/z_v3_x.csv。
/分类程序/separate_z_free.py是对放开红移拟合结果“/输出/z_free_slim.csv”，使用分类准则完整11个步骤的分类程序，分类完成得到参数type_xie，把它添加到原读写文件“/输出/z_free_slim.csv”中，并另存为分类结果文件：/分类结果/z_free.csv。
