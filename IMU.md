### 标定
imu_utils和kalibr_allan标定出来的acc_n,gyr_n,acc_w和gyr_w都是连续时间下的。即

gyr_w: $\frac{rad}{s}\sqrt{Hz}$
acc_w: $\frac{m}{s^2}\sqrt{Hz}$
gyr_n: $\frac{rad}{s}\frac{1}{\sqrt{Hz}}$
acc_n: $\frac{m}{s^2}\frac{1}{\sqrt{Hz}}$

要替换为离散时间下，需要进行

$\Delta t$ is the inverse of the sampling frequency
acc_w_d = acc_w * $\sqrt{\Delta t}$
gyr_w_d = gyr_w * $\sqrt{\Delta t}$
acc_n_d = acc_n / $\sqrt{\Delta t}$
gyr_n_d = gyr_n / $\sqrt{\Delta t}$

假定IMU采样频率是200Hz，那么

acc_w_d = acc_w / $\sqrt{200}$
gyr_w_d = gyr_w / $\sqrt{200}$
acc_n_d = acc_n * $\sqrt{200}$
gyr_n_d = gyr_n * $\sqrt{200}$