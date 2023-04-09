### enum类型的变量不能由整型变量赋值，那么该如果从.yaml加载参数并将其赋值给enum类型变量

你可以在从 YAML 文件加载参数后，使用映射表（map）将整数值或字符串值转换为相应的 enum 类型。以下是一个简单的示例，展示如何从 YAML 文件加载参数，并将其转换为 enum 类型的变量。

首先，假设你有一个名为 Color 的 enum 类型：

        enum Color {
            RED = 0,
            GREEN = 1,
            BLUE = 2
        };

然后，假设你有一个名为 config.yaml 的 YAML 文件，包含以下内容：

        color: 1

你可以使用以下代码从 YAML 文件加载参数，并将其转换为 enum 类型的变量：

        #include <iostream>
        #include <map>
        #include <yaml-cpp/yaml.h>

        enum Color {
            RED = 0,
            GREEN = 1,
            BLUE = 2
        };

        int main() {
            // 加载 YAML 文件
            YAML::Node config = YAML::LoadFile("config.yaml");

            // 从 YAML 文件中获取整数值
            int color_value = config["color"].as<int>();

            // 创建一个映射表，将整数值映射到相应的 enum 类型
            std::map<int, Color> color_map = {
                {0, RED},
                {1, GREEN},
                {2, BLUE}
            };

            // 使用映射表将整数值转换为 enum 类型
            Color color = color_map[color_value];

            // 输出结果
            std::cout << "Color: " << color << std::endl;

            return 0;
        }


