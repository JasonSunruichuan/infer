# Copyright (c) 2016 - present Facebook, Inc.
# All rights reserved.
#
# This source code is licensed under the BSD style license found in the
# LICENSE file in the root directory of this source tree. An additional grant
# of patent rights can be found in the PATENTS file in the same directory.

TESTS_DIR = ../..
ROOT_DIR = $(TESTS_DIR)/../..

ANALYZER = infer
SOURCES_DIR = $(ROOT_DIR)/examples/java_hello
SOURCES = $(wildcard $(SOURCES_DIR)/*.java)
# no objects since we only run a mock gradle that cannot compile Java sources
OBJECTS =
INFERPRINT_OPTIONS = --issues-tests

include $(TESTS_DIR)/java.make
include $(TESTS_DIR)/base.make

infer-out/report.json: $(JAVA_DEPS) $(SOURCES)
#	mock version of gradle
	PATH=$(CURDIR)/../mock:"$$PATH"; \
	cd $(SOURCES_DIR) && \
	$(call silent_on_success,\
	  $(INFER_BIN) -a $(ANALYZER) --results-dir $(CURDIR)/infer-out -- gradle build)
