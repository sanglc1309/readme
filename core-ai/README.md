# Core AI Document

## Table of content

- [1. Installation (Cài đặt)](#installation)
- [2. Overview (Tổng quan)](#overview)

  - [Eocortex (Thông tin Server)](#eocortex)
  - [Eocortex Hook App (Ứng dụng của server)](#eocortex-hook-app)
  - [Key Provider (Bộ cung cấp key)](#key-provider)
  - [Registered Eocortex Hook Event (Sự kiện đăng ký)](#registered-eocortex-hook-event)
  - [Archive Event (Danh sách sự kiện đã lưu)](#archive-event)
  - [Eocortex Client](#eocortex-client)
    - [Get Channel (Danh sách camera)](#get-channels)
    - [Live Url](#get-live-url)
    - Điều khiển camera
  - Statistic (Thống kê)
  - Report (Báo cáo)

- [3. Tutorial (Hướng dẫn)](#tutorial)
  - [Web/App Manager](#1-webapp-manager)
  - [Third-party](#2-third-party)

## Installation

This document is for the latest Core AI 1.0 release and later.

[API Document](http://202.78.227.175:32374/swagger/index.html)

**Authorization type:** Bearer Token

Thay thế với Gateway API:

> digitrans-ai-api.bakco.vn/v1/core-ai/{everything}

**`Ví dụ`**

```text
- http://202.78.227.175:32374/v1/{everything}
- https://digitrans-ai-api.bakco.vn/v1/core-ai/{everything}
```

## Overview

### Eocortex

---

**_Thông tin server camera_**

- Tạo thông tin server của tài khoản quản lý đang đăng nhập
- Một tài khoản thêm được nhiều server

| Tên trường | Mô tả             |
| ---------- | ----------------- |
| `username` | Tài khoản kết nối |
| `password` | Mật khẩu kết nối  |

### Eocortex Hook App

---

**_Tạo App hoạt động cho server_**

- Một server có thể nhiều App cho việc phân quyền nhận sự kiện

| Tên trường   | Mô tả                                    |
| ------------ | ---------------------------------------- |
| `appName`    | Tên ứng dụng                             |
| `eventHook`  | Địa chỉ cấu hình webhook để nhận sự kiện |
| `eocortexId` | Id của server                            |

### Key Provider

---

**_Key truy cập Eocortex App_**

- Tài khoản quản lý tạo ra một hoặc nhiều key cho ứng dụng. Sau đó, người quản lý sử dụng key cho việc gọi API ở các phần mềm thứ 3 thay vì sử dụng mật khẩu.
- Key có thời gian hết hạn hoặc không.

| Tên trường          | Mô tả             |
| ------------------- | ----------------- |
| `description`       | Mô tả             |
| `expiredDate`       | Thời gian hết hạn |
| `eocortexHookAppId` | Id của ứng dụng   |

### Registered Eocortex Hook Event

---

**_Các sự kiện đã đăng ký_**

- Đăng ký các sự kiện cho ứng dụng đã tạo

1. Lấy danh sách sự kiện đã đăng ký

   > /v1/RegisteredEocortexHookEvent/GetRegisteredEventsByAppId/{appId}

   - isHookEnabled = true (Đã đăng ký), = false (Chưa đăng ký)

2. Đăng ký sự kiện

   > /v1/RegisteredEocortexHookEvent/UpdateListByAppId/{appId}

   - Truyền danh sách Id sự kiện đăng ký (có isHookEnabled = true)

3. Đăng ký tất cả sự kiện
   > /v1/RegisteredEocortexHookEvent/RegisterAll/{appId}

### Archive Event

---

**_Sự kiện đã lưu_**

| Tên trường         | Mô tả                              |
| ------------------ | ---------------------------------- |
| `id`               | Mã                                 |
| `host`             | Địa chỉ server                     |
| `eventId`          | Mã của sự kiện                     |
| `eventDescription` | Loại sự kiện                       |
| `channelId`        | Mã của kênh camera                 |
| `channelName`      | Tên của kênh camera                |
| `timeStamp`        | Thời gian                          |
| `group`            | Thuộc nhóm (White list/ Blacklist) |

### Eocortex Client

---

#### Get channels

**_Lấy danh sách camera_**

Sử dụng key

> /v1/EocortexClient/GetChannels

Sử dụng token

> /v1/EocortexClient/Auth/GetChannels/{eocortexId}

#### Get Live Url

**_Lấy đường dẫn trực tiếp của camera_**

Sử dụng key

> /v1/EocortexClient/GetLiveUrl/{channelId}

Sử dụng token

> /v1/EocortexClient/Auth/GetLiveUrl/{eocortexId}/{channelId}

## Tutorial

---

### 1. Web/App Manager

- Sử dụng tài khoản được cấp bởi Admin để request

```console
- Quản lý thông tin server
- Quản lý thông tin ứng dụng
- Quản lý thông tin key của ứng dụng
- Phân quyền sự kiện cho các ứng dụng
- Hiển thị video trực tuyến của danh sách camera
- Hiển thị danh sách sự kiện của server
- Thống kê báo cáo
```

### 2. Third-party

- Sử dụng key được cấp để request

```console
- Hiển thị video trực tuyến của danh sách camera
- Hiển thị danh sách sự kiện của server
```
