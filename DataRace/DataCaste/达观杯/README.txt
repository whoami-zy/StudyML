分类 19 类 这是一个多分类问题  数据提供了文本，有基于字和词的两种数据，但是都经过了脱敏，全是以数字表示。

排名：7 / 3700

总结：抱了大佬了，大佬主要是使用NN做模型，我使用传统的机器学习模型做，最终使用两者模型融合

学习： 传统的机器学习模型特征提取。
	基于字的，这里我没有使用。
	基于词的，采用了:
		tfidf:  ngram(1,2) (ngram_range=(1,2),min_df=3, max_df=0.9,use_idf=1,smooth_idf=1, sublinear_tf=1,max_features=400000,analyzer='word')
				ngram(1,1) (ngram_range=(1,1),min_df=3, max_df=0.9,use_idf=1,smooth_idf=1, sublinear_tf=1,max_features=400000,analyzer='word')
				ngram(3,3) (ngram_range=(3,3),min_df=3, max_df=0.9,use_idf=1,smooth_idf=1, sublinear_tf=1,max_features=400000,analyzer='word')
				ngram(4,4) (ngram_range=(4,4),min_df=3, max_df=0.9,use_idf=1,smooth_idf=1, sublinear_tf=1,max_features=400000,analyzer='word')
				ngram(1,2) (ngram_range=(1,2),min_df=3,use_idf=1,smooth_idf=1, sublinear_tf=1,max_features=10000,analyzer='char')
				加了文章长度特征 docLen
				特征合并：hstack([trn_term_doc,trn_term_word,trn_term_word_three,trn_term_word_four,doclen_word]).tocsr()
			LinearSVC 模型训练
				线下：786
				线上：779多 排名90+
		尝试过在tfidf的基础上使用svd进行降维，但是效果下降。
		在tfidf的基础上 添加 CountVectorizer 特征，模型没有之前收敛，更高维度，分数降低。单独使用CountVectorizer特征，模型过拟合。效果也没有tfidf效果好。

经验与不足： 第一次做NLP,之前虽然也有了解过，但是第一次正经做，没有尝试使用更多的机器学习模型，单单只使用了svc，单模型。在后面的比赛中2018CCF中使用了多模型进行stacking，模型提升了一个百，效果还是很不错的。做这个比赛的时候还不太会使用stacking技术，在后面的比赛中，要擅长使用该方法。模型融合远比单模型的效果要好。

大佬的NN思路：
	NN,还不太熟悉，等有机会总结下。


前十大佬的特征思路在PDF里，总结下。

最后还是传统的和NN进行bleding融合，效果可观。
