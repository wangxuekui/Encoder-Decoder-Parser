This implementation is based on the [dynet2.0 library](https://github.com/clab/dynet) for this software to function. The paper is "Encoder-Decoder Shift-Reduce Syntactic Parsing".

### Building

    mkdir build
    cd build
    cmake .. -DEIGEN3_INCLUDE_DIR=/path/to/eigen
    make    

Add -DBACKEND=cuda to cmake for GPU compile. 

### Data

The preparation of training, development and test data are the same as the work of [stack-LSTM](https://github.com/clab/lstm-parser) on dependency parsing, and the work of [recurrent neural network grammar](https://github.com/clab/rnng) on constituent parsing. After that, the training, development and test oracle files could be got.

### Training

Dependency parsing

    ./dependency-parser --dynet-mem 2400 --train_file [training oracle] --dev_file [development oracle] --words_file [pretrained word embeddings] --layers 2 --action_dim 40 --input_dim 64 --pos_dim 6 --pretrained_dim 100 --rel_dim 20 --bilstm_input_dim 100 --bilstm_hidden_dim 200 --attention_hidden_dim 50 --train_methods 3 --train --use_pos --unk_strategy --unk_prob 0.2 --pdrop 0.3 

Constituent parsing

    ./constituent-parser -T [training oracle] -d [development oracle] -C [development data in bracketed format]--layers 2 --input_dim 64 --pos_dim 6 --bilstm_input_dim 100 --bilstm_hidden_dim 200 --attention_hidden_dim 50 -w [pretrained word embeddings] --pretrained_dim 100 --action_dim 40 -t -P -D 0.5 --dynet-mem 1700

### Decoding

Dependency parsing

    ./dependency-parser --dynet-mem 2400 --train_file [training oracle] --dev_file [test oracle] --words_file [pretrained word embeddings] --layers 2 --action_dim 40 --input_dim 64 --pos_dim 6 --pretrained_dim 100 --rel_dim 20 --bilstm_input_dim 100 --bilstm_hidden_dim 200 --attention_hidden_dim 50 --train_methods 3 --use_pos

Constituent parsing

    ./constituent-parser -T [training oracle] -p [test oracle] -C [test data in bracketed format] --layers 2 --input_dim 64 --pos_dim 6 --bilstm_input_dim 100 --bilstm_hidden_dim 200 --attention_hidden_dim 50 -w [pretrained word embeddings] --pretrained_dim 100 --action_dim 40 -P --dybet-mem 1700 -m [model]

### Cite

    @article{liu2017encoder,
  	title={Encoder-Decoder Shift-Reduce Syntactic Parsing},
  	author={Liu, Jiangming and Zhang, Yue},
  	journal={arXiv preprint arXiv:1706.07905},
  	year={2017}
    	}


