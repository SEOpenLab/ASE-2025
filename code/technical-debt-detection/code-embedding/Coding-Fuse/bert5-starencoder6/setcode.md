python run.py \
    --output_dir=./saved_models \
    --model_type=auto \
    --tokenizer_name=./starencoder \
    --model_name_or_path=./starencoder \
    --do_train \
    --train_data_file=../dataset/train.jsonl \
    --eval_data_file=../dataset/valid.jsonl \
    --test_data_file=../dataset/test.jsonl \
    --epoch 100 \
    --early_stopping_patience 10 \
    --block_size 50 \
    --train_batch_size 16 \
    --eval_batch_size 64 \
    --learning_rate 1e-1 \
    --max_grad_norm 1.0 \
    --evaluate_during_training \
    --seed 123456  2>&1 | tee train.log && python run.py \
    --output_dir=./saved_models \
    --model_type=auto \
    --tokenizer_name=./starencoder \
    --model_name_or_path=./starencoder \
    --do_eval \
    --do_test \
    --train_data_file=../dataset/train.jsonl \
    --eval_data_file=../dataset/valid.jsonl \
    --test_data_file=../dataset/test.jsonl \
    --epoch 100 \
    --early_stopping_patience 10 \
    --block_size 50 \
    --train_batch_size 16 \
    --eval_batch_size 64 \
    --learning_rate 1e-1 \
    --max_grad_norm 1.0 \
    --evaluate_during_training \
    --seed 123456 2>&1 | tee test.log && python ../evaluator/evaluator.py -a ../dataset/test.jsonl -p saved_models/predictions.txt
