# History
This is a practice to test BERT for Chinese Word Segmentation task.

## Test classifier
python run_classifier_torch.py

## Test Chinese Word Segmentation with BERT
python main.py

### Input format for the Ontonotes dataset
*   bert_ner	bert_seg	full_pos	src_ner	src_seg	text	text_seg
>  An example
>      s = '(NP (CP (IP (NP (DNP (NER-GPE (NR Taiwan)) (DEG 的)) (NER-ORG (NR 公视))) (VP (NT 今天) (VV 主办))) (DEC 的)) (NP-m (NP (NR 台北) (NN 市长)) (NP-m (NP (NN candidate) (NN defence)) (PU ，))))'
>      bert_ner: W-GPE O B-ORG E-ORG B E B E O B E B E B M M E B M E O
>      bert_seg: S S B E B E B E S B E B E B M M E B M E S
>      full_pos: (NP (CP (IP (NP (DNP (NR )NR )DNP (DEG )DEG )NP (NR )NR )IP )CP (VP (NT )NT (VV )VV )VP )NP (DEC )DEC )DEC (NP-m (NP (NR )NR (NN )NN )NP (NP-m (NP (NN )NN (NN )NN )NP (PU )PU )NP-m )NP-m )NP-m
>      src_ner: W-GPE,O,B-ORG,E-ORG,B,E,B,E,O,B,E,B,E,O,O,O,
>      src_seg: S,S,B,E,B,E,B,E,S,B,E,B,E,S,S,S,
>      text: Taiwan的公视今天主办的台北市长candidate defence，
>      text_seg: Taiwan 的 公视 今天 主办 的 台北 市长 candidate defence ，

### Input format for the four CWS datasets: AS, CityU, MSR, PKU
*   bert_seg	full_pos	src_seg	text	text_seg
>  An example
>      s = '目前　由　２３２　位　院士　（　Ｆｅｌｌｏｗ　及　Ｆｏｕｎｄｉｎｇ　Ｆｅｌｌｏｗ　）　，６６　位　協院士　（　Ａｓｓｏｃｉａｔｅ　Ｆｅｌｌｏｗ　）　２４　位　通信　院士　（　Ｃｏｒｒｅｓｐｏｎｄｉｎｇ　Ｆｅｌｌｏｗ　）　及　２　位　通信　協院士　（　Ｃｏｒｒｅｓｐｏｎｄｉｎｇ　Ａｓｓｏｃｉａｔｅ　Ｆｅｌｌｏｗ　）　組成　（　不　包括　一九九四年　當選　者　）　，'
>      bert_seg: S S B E B E B E S B E B E B M M E B M E S
>      src_seg: S,S,B,E,B,E,B,E,S,B,E,B,E,S,S,S,
>      text: 目前由２３２位院士（Ｆｅｌｌｏｗ及Ｆｏｕｎｄｉｎｇ　Ｆｅｌｌｏｗ），６６位協院士（Ａｓｓｏｃｉａｔｅ　Ｆｅｌｌｏｗ）２４位通信院士（Ｃｏｒｒｅｓｐｏｎｄｉｎｇ　Ｆｅｌｌｏｗ）及２位通信協院士（Ｃｏｒｒｅｓｐｏｎｄｉｎｇ　Ａｓｓｏｃｉａｔｅ　Ｆｅｌｌｏｗ）組成（不包括一九九四年當選者），
>      text_seg: 目前　由　２３２　位　院士　（　Ｆｅｌｌｏｗ　及　Ｆｏｕｎｄｉｎｇ　Ｆｅｌｌｏｗ　）　，６６　位　協院士　（　Ａｓｓｏｃｉａｔｅ　Ｆｅｌｌｏｗ　）　２４　位　通信　院士　（　Ｃｏｒｒｅｓｐｏｎｄｉｎｇ　Ｆｅｌｌｏｗ　）　及　２　位　通信　協院士　（　Ｃｏｒｒｅｓｐｏｎｄｉｎｇ　Ａｓｓｏｃｉａｔｅ　Ｆｅｌｌｏｗ　）　組成　（　不　包括　一九九四年　當選　者　）　，

## BertCWSDemo.py needs files
>   src/BERT/*
>   in src: config.py, customize_modeling.py, preprocess.py, tokenization.py, TorchCRF.py, utilis.py
>
> text = '''
>        款款好看的美甲，简直能搞疯“选择综合症”诶！。这是一组超级温柔又带点设计感的美甲💅。
>        春天来了🌺。美甲也从深色系转变为淡淡的浅色系了💐。今天给大家推荐最适合春天的美甲💅。
>        希望你们会喜欢~😍@MT小美酱 @MT情报局 @美图秀秀 #春季美甲##显白美甲##清新美甲##ins美甲#
>      '''
> outputT = model.cutlist_noUNK([text])
> output = [' '.join(lst) for lst in outputT]
> o = ''
> for x in output: o += x + '\t'
> print(o+'\n')
> o = '''
>   款款 好看 的 美甲 ， 简直 能 搞疯 “ 选择 综合症 ” 诶 ！ 。 这 是 一 组 超级 温柔 又 带 点 设计感 的
>   美甲 💅 。 春天 来 了 🌺 。 美甲 也 从 深 色系 转变 为 淡淡 的 浅 色系 了 💐 。 今天 给 大家 推荐
>   最 适合 春天 的 美甲 💅 。 希望 你们 会 喜欢 ~ 😍 @ MT 小美酱 @ MT 情报局 @ 美图 秀秀 # 春季 美甲 # # 显白 美甲 # # 清新 美甲 # # ins 美甲 #
> '''

