load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
  name = 'libgeos',
  url = 'https://github.com/libgeos/geos/archive/3133734b73aec52c70643c41fc43f19cfb5f680f.tar.gz',
  strip_prefix = 'geos-3133734b73aec52c70643c41fc43f19cfb5f680f',
  sha256 = 'e8cf6bfbcec34a69c3628a9931c83c1dedaf7ae91088cda19d8150cbda10264f',
  build_file = '@//:third-party/geos/BUILD',
)
