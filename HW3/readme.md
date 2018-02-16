
# Word Embedding

Open your VM and download the jupyter notebook file and BEST2010 data

Note that this BEST2010 dataset has not been preprocessed, it contains the same content as the one on NECTEC's website.  You might have to move your previous BEST2010 dataset elsewhere. 

```
mv BEST2010 BEST2010-prev
wget --no-check-certificate https://raw.githubusercontent.com/ekapolc/nlp_course/master/HW3/thai_skip_gram_demo.ipynb
wget --no-check-certificate https://raw.githubusercontent.com/ekapolc/nlp_course/master/HW3/thai_skip_gram_homework_for_student.ipynb
wget --no-check-certificate https://github.com/ekapolc/nlp_course/raw/master/HW3/BEST2010.zip
unzip BEST2010.zip
cd /data
wget --no-check-certificate https://www.dropbox.com/s/rbhufb6uy22k338/my_skipgram32_weights.h5
```

If you have issue with character encoding, you might have to do the following:
```
import codecs
with codec.open(cwd+"/corpora/wiki/thwiki_chk.txt", encoding='utf-8') as f:
	......
```

Submit the completed notebook file on MyCourseVille (4.5 points total, 0.75 points per 1 TODO)

Submit a screenshot of the closed instance (0.5 points)


## Acknowledgements

We would like to thank Natthawut Kertkeidkachorn for providing the Wikipedia data.
