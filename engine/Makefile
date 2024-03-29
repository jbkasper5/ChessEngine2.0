SRC_DIR=src
BIN_DIR=bin
DEBUG_BIN_DIR=$(BIN_DIR)/debug
SRCS=$(shell find $(SRC_DIR)/*.c)
TOBJS=$(patsubst %.c, %.o, $(SRCS))
OBJS=$(patsubst $(SRC_DIR)/%, $(BIN_DIR)/%, $(TOBJS))
DOBJS=$(patsubst $(BIN_DIR)/%, $(DEBUG_BIN_DIR)/d_%, $(OBJS))
DEBUG=-DDEBUG
INCLUDE_PATH=include/

CC=				gcc
OPT=			-O3
CFLAGS=			-g -std=c11
TARGET=			engine
DTARGET=		d$(TARGET)

all: $(BIN_DIR) $(TARGET)

.PHONY: re
re: clean all

.PHONY: debug
debug: $(DEBUG_BIN_DIR) $(DTARGET)

$(TARGET): $(OBJS)
	$(CC) $^ -o $@ $(CFLAGS) -I $(INCLUDE_PATH)

$(DTARGET): $(DOBJS)
	$(CC) $^ -o $@ $(CFLAGS) -I $(INCLUDE_PATH)

$(BIN_DIR)/%.o: $(SRC_DIR)/%.c
	$(CC) -c $< -o $@ $(CFLAGS) -I $(INCLUDE_PATH)

$(DEBUG_BIN_DIR)/d_%.o: $(SRC_DIR)/%.c
	$(CC) -c $< -o $@ $(CFLAGS) $(DEBUG) -I $(INCLUDE_PATH)

$(BIN_DIR) $(DEBUG_BIN_DIR):
	mkdir -p $@

.PHONY: clean
clean:
	$(RM) -rf $(TARGET)
	$(RM) -rf $(DTARGET)
	$(RM) -rf $(BIN_DIR)