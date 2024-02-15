# Context Helps Determine Spatial Knowledge from Tweets

This repository will contain the corpus of the Findings AACL 2023 paper 
"Context Helps Determine Spatial Knowledge from Tweets"  
Authors: Zhaomin Xiao, Yan Huang, and Eduardo Blanco

You can find our corpus in this repository.
**Note that we remove user data, such as profile image and username, to avoid potential privacy issue. Our corpus only contains tweet text and corresponding annotations.**

To replicate our experiments with large language models, you need to ensure you have enough space to download the pretrained weights of LLMs, whose sizes range from 5G to 40G.
Additionally, since the models we used in our experiments are hosted by Huggingface, you need to check if you have correctly installed Huggingface.

Regarding the experiments with ChatGPT, the results were obtained in Oct 2023. Therefore, it is possible that it was not replicable due to the model upgrade on the OpenAI side.
Also, please be mindful that instruction finetuning with ChatGPT is costly, as we spent more than $500 on the experiments of instruction finetuning.

If you have any questions about the paper and code&data, please contact me via email: zhaominxiao@my.unt.edu

## Citation

If you want to use the corpus, please cite the paper below.
```bibtex
@inproceedings{xiao-etal-2023-context,
    title = "Context Helps Determine Spatial Knowledge from Tweets",
    author = "Xiao, Zhaomin  and
      Huang, Yan  and
      Blanco, Eduardo",
    editor = "Park, Jong C.  and
      Arase, Yuki  and
      Hu, Baotian  and
      Lu, Wei  and
      Wijaya, Derry  and
      Purwarianti, Ayu  and
      Krisnadhi, Adila Alfa",
    booktitle = "Findings of the Association for Computational Linguistics: IJCNLP-AACL 2023 (Findings)",
    month = nov,
    year = "2023",
    address = "Nusa Dua, Bali",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2023.findings-ijcnlp.13",
    pages = "149--160",
}
```

