## Fine-tuning for Dacon AI Competition  
BEiT-3를 비롯한 다른 모델을 Git Clone해서 구글 드라이브에 저장한 후, 수정한 코드만 따로 Git에 저장하였습니다.  
  ### 수정 내용   
  1. dataset.py : CustomDataset Class 추가 및 task2dataset에 vqacustom 추가  
  2. utils.py : import torch._six를 torch로 수정(module not found 에러 해결), pos_tokens = pos_tokens.float() 코드 추가(575번째 줄), dump_prediction 함수   
                (838번째 줄)에 있는 torch.distributed.barrier() 삭제(single GPU에서의 eval 위함, multi GPU의 경우 삭제 안해도 됨)  
  3. engine_for_finetuning.py : def get_handler 함수에(442번째 줄) args.task == "vqacustom" 추가  
  4. modeling_finetune.py : vqacustom 모델들 추가 및 num_classes부분 수정(label 수에 맞게)  
  5. run_beit3_finetuning.py : parser.add_argument --task 부분에 vqacustom 추가, args.eval(357번째 줄)에 vqacustom 부분(367~370번째 줄) 추가  
  
  
## Citation  
```
@inproceedings{beit3,
title={Image as a foreign language: {BEiT} pretraining for vision and vision-language tasks},
author={Wenhui Wang and Hangbo Bao and Li Dong and Johan Bjorck and Zhiliang Peng and Qiang Liu and Kriti Aggarwal and Owais Khan Mohammed and Saksham Singhal and Subhojit Som and Furu Wei},
booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
year={2023}
}

@article{beitv2,
title={{BEiT v2}: Masked Image Modeling with Vector-Quantized Visual Tokenizers},
author={Zhiliang Peng and Li Dong and Hangbo Bao and Qixiang Ye and Furu Wei},
year={2022},
eprint={2208.06366},
archivePrefix={arXiv},
primaryClass={cs.CV}
}

@inproceedings{beit,
title={{BEiT}: {BERT} Pre-Training of Image Transformers},
author={Hangbo Bao and Li Dong and Songhao Piao and Furu Wei},
booktitle={International Conference on Learning Representations},
year={2022},
url={https://openreview.net/forum?id=p-BhZSz59o4}
}
```  
  
