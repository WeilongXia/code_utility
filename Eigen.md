### Eigen初始化一个7*13的矩阵
在Eigen库中，可以使用Eigen::MatrixXd类来创建一个动态大小的矩阵。要初始化一个7x13的矩阵，可以使用以下代码：

        #include <Eigen/Dense>

        int main()
        {
            Eigen::MatrixXd H(7, 13);
            H.setZero(); // 设置矩阵中的所有元素为0
        }

在这个例子中，我们创建了一个7x13的矩阵H，并将其所有元素初始化为0。Eigen::MatrixXd可以用于表示任意大小的矩阵。如果在编译时知道矩阵大小，也可以使用Eigen::Matrix<double, Rows, Cols>类。


### Eigen给一个4*3矩阵赋值
在Eigen中，给一个4x3矩阵赋值可以通过多种方式。下面是一些常见的赋值方法：
* 逐个元素赋值：

        #include <iostream>
        #include <Eigen/Dense>
        int main() {
            Eigen::Matrix<double, 4, 3> A;

            A(0, 0) = 1.0;
            A(0, 1) = 2.0;
            A(0, 2) = 3.0;
            A(1, 0) = 4.0;
            A(1, 1) = 5.0;
            A(1, 2) = 6.0;
            A(2, 0) = 7.0;
            A(2, 1) = 8.0;
            A(2, 2) = 9.0;
            A(3, 0) = 10.0;
            A(3, 1) = 11.0;
            A(3, 2) = 12.0;

            std::cout << "Matrix A:\n" << A << std::endl;
        }

* 使用<<操作符一次性赋值：

        #include <iostream>
        #include <Eigen/Dense>

        int main() {
            Eigen::Matrix<double, 4, 3> A;

            A << 1.0, 2.0, 3.0,
                4.0, 5.0, 6.0,
                7.0, 8.0, 9.0,
                10.0, 11.0, 12.0;

            std::cout << "Matrix A:\n" << A << std::endl;
        }

* 使用comma-initializer语法一次性赋值：

        #include <iostream>
        #include <Eigen/Dense>

        int main() {
            Eigen::Matrix<double, 4, 3> A;

            A = (Eigen::Matrix<double, 4, 3>() << 1.0, 2.0, 3.0,
                                                4.0, 5.0, 6.0,
                                                7.0, 8.0, 9.0,
                                                10.0, 11.0, 12.0).finished();

            std::cout << "Matrix A:\n" << A << std::endl;
        }

### Eigen四元数初始化的方式有哪几种

* 通过四个标量进行初始化

        Eigen::Quaterniond q(w, x, y, z);

* 通过Eigen向量进行初始化

        Eigen::Quaterniond q(Eigen::Vector4d(x, y, z, w))

* 通过标量部分和向量部分初始化：

        double w = 1.0;
        Eigen::Vector3d vec(0.0, 0.0, 0.0);
        Eigen::Quaterniond q(w, vec(0), vec(1), vec(2));

* 通过旋转矩阵（3x3矩阵）初始化：

        Eigen::Matrix3d rot_matrix;
        // 填充旋转矩阵的元素
        Eigen::Quaterniond q(rot_matrix);

* 通过欧拉角（Yaw, Pitch, Roll）初始化：

        double yaw = 0.0, pitch = 0.0, roll = 0.0;
        Eigen::Quaterniond q;
        q = Eigen::AngleAxisd(yaw, Eigen::Vector3d::UnitZ()) *
            Eigen::AngleAxisd(pitch, Eigen::Vector3d::UnitY()) *
            Eigen::AngleAxisd(roll, Eigen::Vector3d::UnitX());

* 通过旋转轴和旋转角度初始化：

        double angle = M_PI / 4;
        Eigen::Vector3d axis(0.0, 0.0, 1.0); // 例如，绕Z轴旋转
        Eigen::Quaterniond q(Eigen::AngleAxisd(angle, axis));


### Eigen四元数元素存放位置是什么样的

通过使用 std::cout << q.coeffs() << std::endl 可以知道，其内部存储是：xyzw

