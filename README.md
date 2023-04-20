# An LSTM network trained online to equalise a rayleigh channel

* An online LSTM estimator estimates channel responses of recieved data symbols. 
* Differing from the channel responses time series that are created by the LSTM training and prediction loop, the channel response series of an online LSTN are composed of the corrected channel responses that are obtained through the recieved data symbols [1]. 
* In this method, tracking of time varying channels can be achieved. 
* Channel estimation is applied on pilots to obtain the channel responses of the pilots for online LSTM training [1].

## Modified process from [1]. 
![LSTM Network Online Training Flowchart](https://github.com/ryan-n-may/Online_LSTM_Cpp/blob/main/LSTM_online_workflow.jpg)

### Offline Training.
1) Pilot aided LS Estimation proivdes the initial h[n].
2) the LSTM network is trained on the pilot aided LS estimation to prime weights. 
### Online Training.
3) Fourier transform is taken of the LSTM network output h'[n]. 
4) Y(z) (rayleigh channel output) is equalised using H'(z) to produce X'(z).
5) LS pilot-aided equalisation is performed on the output X'(z) to produce X(z) and H(z).
6) Error 'ε' is calculated between H(z) and H'(z).
7) LSTM is updated via BPTT (back propagation through time) using error ε.
8) Input to LSTM is H(z).
9) Process repeats from stage (3).  

## Detailed process of whole system.
![image](https://github.com/ryan-n-may/Online_LSTM_Cpp/blob/main/LSTM_complete_system.jpg)

## Detiled process of whole system in MIMO configuration. 
The benefits of a MIMO process include the use of a DNN (such as DIP [2]) to denoise the equalisation output. 
![image](https://github.com/ryan-n-may/Online_LSTM_Cpp/blob/main/LSTM_complete_system_MIMO.jpg)


[1] https://ieeexplore.ieee.org/abstract/document/9144225 (LSTM Online training model).  
[2] https://arxiv.org/abs/1711.10925 (DIP). 
 
