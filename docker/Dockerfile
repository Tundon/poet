FROM nvcr.io/nvidia/pytorch:22.01-py3

# Install mish-cuda required for YOLOv4
RUN git clone https://github.com/JunnYu/mish-cuda /packages/mish-cuda
WORKDIR /packages/mish-cuda
RUN python setup.py build install
# Install Deformable DETR

RUN git clone https://github.com/fundamentalvision/Deformable-DETR.git /packages/Deformable-DETR
WORKDIR /packages/Deformable-DETR/models/ops/
RUN python setup.py build install

WORKDIR /workspace/poet
