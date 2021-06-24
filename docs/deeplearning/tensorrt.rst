tensorrt 学习笔记
=================

#. nvinfer1:Dims 表示的是CHW的各个纬度，而不是NCHW！

#. ModelImporter 类实现了nvonnxparser::IParser

#. onnx parser 中增加对插件的支持，需要修改 builtin_op_importers.cpp

#. 增加插件后，需要在文件 InferPlugin.cpp 注册插件
