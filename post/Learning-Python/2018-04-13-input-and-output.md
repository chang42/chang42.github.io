
# 文件读写（Input and Output）  
在文件中读出或者写入的必须为字符串，其他形式需转为字符串。  
首先，写入文件：


```python
f = open('file.txt', 'w')
```


```python
type(f)
```




    _io.TextIOWrapper




```python
f.write('This is a test \nand another test')
```




    32




```python
f.close()
```

读出文件：


```python
f = open('file.txt', 'r')
```


```python
s = f.read()
```


```python
print(s)
```

    This is a test 
    and another test
    


```python
f.close()
```

迭代文件：


```python
f = open('file.txt', 'r')
```


```python
for line in f:
    print(line)
```

    This is a test 
    
    and another test
    


```python
f.close()
```

文件读写模式：  
* `r` : 只读
* `w` : 只写，如果文件已经存在，会覆盖之前的内容
* `a` : 添加，不覆盖之前的内容
* `r+/w+` : 读和写
* `b` : 二进制模式  

## 关闭文件  
在Python中，如果一个打开的文件不再被其他变量引用时，它会自动关闭这个文件。  
所以正常情况下，如果一个文件正常被关闭了，忘记调用文件的 `close` 方法不会有什么问题。  
关闭文件可以保证内容已经被写入文件，而不关闭可能会出现意想不到的结果：  


```python
f = open('newfile.txt', 'w')
f.write('You should close the file!')
g = open('newfile.txt', 'r')
print(repr(g.read()))
```

    ''
    

虽然这里写了内容，但是在关闭之前，这个内容并没有被写入磁盘。  
使用循环写入的内容也并不完整：


```python
f = open('newfile.txt','w')
for i in range(1000):
    f.write('You should close the file: ' + str(i) + '\n')

g = open('newfile.txt', 'r')
print(g.read())
f.close()
g.close()
```

    You should close the file: 0
    You should close the file: 1
    You should close the file: 2
    You should close the file: 3
    You should close the file: 4
    You should close the file: 5
    You should close the file: 6
    You should close the file: 7
    You should close the file: 8
    You should close the file: 9
    You should close the file: 10
    You should close the file: 11
    You should close the file: 12
    You should close the file: 13
    You should close the file: 14
    You should close the file: 15
    You should close the file: 16
    You should close the file: 17
    You should close the file: 18
    You should close the file: 19
    You should close the file: 20
    You should close the file: 21
    You should close the file: 22
    You should close the file: 23
    You should close the file: 24
    You should close the file: 25
    You should close the file: 26
    You should close the file: 27
    You should close the file: 28
    You should close the file: 29
    You should close the file: 30
    You should close the file: 31
    You should close the file: 32
    You should close the file: 33
    You should close the file: 34
    You should close the file: 35
    You should close the file: 36
    You should close the file: 37
    You should close the file: 38
    You should close the file: 39
    You should close the file: 40
    You should close the file: 41
    You should close the file: 42
    You should close the file: 43
    You should close the file: 44
    You should close the file: 45
    You should close the file: 46
    You should close the file: 47
    You should close the file: 48
    You should close the file: 49
    You should close the file: 50
    You should close the file: 51
    You should close the file: 52
    You should close the file: 53
    You should close the file: 54
    You should close the file: 55
    You should close the file: 56
    You should close the file: 57
    You should close the file: 58
    You should close the file: 59
    You should close the file: 60
    You should close the file: 61
    You should close the file: 62
    You should close the file: 63
    You should close the file: 64
    You should close the file: 65
    You should close the file: 66
    You should close the file: 67
    You should close the file: 68
    You should close the file: 69
    You should close the file: 70
    You should close the file: 71
    You should close the file: 72
    You should close the file: 73
    You should close the file: 74
    You should close the file: 75
    You should close the file: 76
    You should close the file: 77
    You should close the file: 78
    You should close the file: 79
    You should close the file: 80
    You should close the file: 81
    You should close the file: 82
    You should close the file: 83
    You should close the file: 84
    You should close the file: 85
    You should close the file: 86
    You should close the file: 87
    You should close the file: 88
    You should close the file: 89
    You should close the file: 90
    You should close the file: 91
    You should close the file: 92
    You should close the file: 93
    You should close the file: 94
    You should close the file: 95
    You should close the file: 96
    You should close the file: 97
    You should close the file: 98
    You should close the file: 99
    You should close the file: 100
    You should close the file: 101
    You should close the file: 102
    You should close the file: 103
    You should close the file: 104
    You should close the file: 105
    You should close the file: 106
    You should close the file: 107
    You should close the file: 108
    You should close the file: 109
    You should close the file: 110
    You should close the file: 111
    You should close the file: 112
    You should close the file: 113
    You should close the file: 114
    You should close the file: 115
    You should close the file: 116
    You should close the file: 117
    You should close the file: 118
    You should close the file: 119
    You should close the file: 120
    You should close the file: 121
    You should close the file: 122
    You should close the file: 123
    You should close the file: 124
    You should close the file: 125
    You should close the file: 126
    You should close the file: 127
    You should close the file: 128
    You should close the file: 129
    You should close the file: 130
    You should close the file: 131
    You should close the file: 132
    You should close the file: 133
    You should close the file: 134
    You should close the file: 135
    You should close the file: 136
    You should close the file: 137
    You should close the file: 138
    You should close the file: 139
    You should close the file: 140
    You should close the file: 141
    You should close the file: 142
    You should close the file: 143
    You should close the file: 144
    You should close the file: 145
    You should close the file: 146
    You should close the file: 147
    You should close the file: 148
    You should close the file: 149
    You should close the file: 150
    You should close the file: 151
    You should close the file: 152
    You should close the file: 153
    You should close the file: 154
    You should close the file: 155
    You should close the file: 156
    You should close the file: 157
    You should close the file: 158
    You should close the file: 159
    You should close the file: 160
    You should close the file: 161
    You should close the file: 162
    You should close the file: 163
    You should close the file: 164
    You should close the file: 165
    You should close the file: 166
    You should close the file: 167
    You should close the file: 168
    You should close the file: 169
    You should close the file: 170
    You should close the file: 171
    You should close the file: 172
    You should close the file: 173
    You should close the file: 174
    You should close the file: 175
    You should close the file: 176
    You should close the file: 177
    You should close the file: 178
    You should close the file: 179
    You should close the file: 180
    You should close the file: 181
    You should close the file: 182
    You should close the file: 183
    You should close the file: 184
    You should close the file: 185
    You should close the file: 186
    You should close the file: 187
    You should close the file: 188
    You should close the file: 189
    You should close the file: 190
    You should close the file: 191
    You should close the file: 192
    You should close the file: 193
    You should close the file: 194
    You should close the file: 195
    You should close the file: 196
    You should close the file: 197
    You should close the file: 198
    You should close the file: 199
    You should close the file: 200
    You should close the file: 201
    You should close the file: 202
    You should close the file: 203
    You should close the file: 204
    You should close the file: 205
    You should close the file: 206
    You should close the file: 207
    You should close the file: 208
    You should close the file: 209
    You should close the file: 210
    You should close the file: 211
    You should close the file: 212
    You should close the file: 213
    You should close the file: 214
    You should close the file: 215
    You should close the file: 216
    You should close the file: 217
    You should close the file: 218
    You should close the file: 219
    You should close the file: 220
    You should close the file: 221
    You should close the file: 222
    You should close the file: 223
    You should close the file: 224
    You should close the file: 225
    You should close the file: 226
    You should close the file: 227
    You should close the file: 228
    You should close the file: 229
    You should close the file: 230
    You should close the file: 231
    You should close the file: 232
    You should close the file: 233
    You should close the file: 234
    You should close the file: 235
    You should close the file: 236
    You should close the file: 237
    You should close the file: 238
    You should close the file: 239
    You should close the file: 240
    You should close the file: 241
    You should close the file: 242
    You should close the file: 243
    You should close the file: 244
    You should close the file: 245
    You should close the file: 246
    You should close the file: 247
    You should close the file: 248
    You should close the file: 249
    You should close the file: 250
    You should close the file: 251
    You should close the file: 252
    You should close the file: 253
    You should close the file: 254
    You should close the file: 255
    You should close the file: 256
    You should close the file: 257
    You should close the file: 258
    You should close the file: 259
    You should close the file: 260
    You should close the file: 261
    You should close the file: 262
    You should close the file: 263
    You should close the file: 264
    You should close the file: 265
    You should close the file: 266
    You should close the file: 267
    You should close the file: 268
    You should close the file: 269
    You should close the file: 270
    You should close the file: 271
    You should close the file: 272
    You should close the file: 273
    You should close the file: 274
    You should close the file: 275
    You should close the file: 276
    You should close the file: 277
    You should close the file: 278
    You should close the file: 279
    You should close the file: 280
    You should close the file: 281
    You should close the file: 282
    You should close the file: 283
    You should close the file: 284
    You should close the file: 285
    You should close the file: 286
    You should close the file: 287
    You should close the file: 288
    You should close the file: 289
    You should close the file: 290
    You should close the file: 291
    You should close the file: 292
    You should close the file: 293
    You should close the file: 294
    You should close the file: 295
    You should close the file: 296
    You should close the file: 297
    You should close the file: 298
    You should close the file: 299
    You should close the file: 300
    You should close the file: 301
    You should close the file: 302
    You should close the file: 303
    You should close the file: 304
    You should close the file: 305
    You should close the file: 306
    You should close the file: 307
    You should close the file: 308
    You should close the file: 309
    You should close the file: 310
    You should close the file: 311
    You should close the file: 312
    You should close the file: 313
    You should close the file: 314
    You should close the file: 315
    You should close the file: 316
    You should close the file: 317
    You should close the file: 318
    You should close the file: 319
    You should close the file: 320
    You should close the file: 321
    You should close the file: 322
    You should close the file: 323
    You should close the file: 324
    You should close the file: 325
    You should close the file: 326
    You should close the file: 327
    You should close the file: 328
    You should close the file: 329
    You should close the file: 330
    You should close the file: 331
    You should close the file: 332
    You should close the file: 333
    You should close the file: 334
    You should close the file: 335
    You should close the file: 336
    You should close the file: 337
    You should close the file: 338
    You should close the file: 339
    You should close the file: 340
    You should close the file: 341
    You should close the file: 342
    You should close the file: 343
    You should close the file: 344
    You should close the file: 345
    You should close the file: 346
    You should close the file: 347
    You should close the file: 348
    You should close the file: 349
    You should close the file: 350
    You should close the file: 351
    You should close the file: 352
    You should close the file: 353
    You should close the file: 354
    You should close the file: 355
    You should close the file: 356
    You should close the file: 357
    You should close the file: 358
    You should close the file: 359
    You should close the file: 360
    You should close the file: 361
    You should close the file: 362
    You should close the file: 363
    You should close the file: 364
    You should close the file: 365
    You should close the file: 366
    You should close the file: 367
    You should close the file: 368
    You should close the file: 369
    You should close the file: 370
    You should close the file: 371
    You should close the file: 372
    You should close the file: 373
    You should close the file: 374
    You should close the file: 375
    You should close the file: 376
    You should close the file: 377
    You should close the file: 378
    You should close the file: 379
    You should close the file: 380
    You should close the file: 381
    You should close the file: 382
    You should close the file: 383
    You should close the file: 384
    You should close the file: 385
    You should close the file: 386
    You should close the file: 387
    You should close the file: 388
    You should close the file: 389
    You should close the file: 390
    You should close the file: 391
    You should close the file: 392
    You should close the file: 393
    You should close the file: 394
    You should close the file: 395
    You should close the file: 396
    You should close the file: 397
    You should close the file: 398
    You should close the file: 399
    You should close the file: 400
    You should close the file: 401
    You should close the file: 402
    You should close the file: 403
    You should close the file: 404
    You should close the file: 405
    You should close the file: 406
    You should close the file: 407
    You should close the file: 408
    You should close the file: 409
    You should close the file: 410
    You should close the file: 411
    You should close the file: 412
    You should close the file: 413
    You should close the file: 414
    You should close the file: 415
    You should close the file: 416
    You should close the file: 417
    You should close the file: 418
    You should close the file: 419
    You should close the file: 420
    You should close the file: 421
    You should close the file: 422
    You should close the file: 423
    You should close the file: 424
    You should close the file: 425
    You should close the file: 426
    You should close the file: 427
    You should close the file: 428
    You should close the file: 429
    You should close the file: 430
    You should close the file: 431
    You should close the file: 432
    You should close the file: 433
    You should close the file: 434
    You should close the file: 435
    You should close the file: 436
    You should close the file: 437
    You should close the file: 438
    You should close the file: 439
    You should close the file: 440
    You should close the file: 441
    You should close the file: 442
    You should close the file: 443
    You should close the file: 444
    You should close the file: 445
    You should close the file: 446
    You should close the file: 447
    You should close the file: 448
    You should close the file: 449
    You should close the file: 450
    You should close the file: 451
    You should close the file: 452
    You should close the file: 453
    You should close the file: 454
    You should close the file: 455
    You should close the file: 456
    You should close the file: 457
    You should close the file: 458
    You should close the file: 459
    You should close the file: 460
    You should close the file: 461
    You should close the file: 462
    You should close the file: 463
    You should close the file: 464
    You should close the file: 465
    You should close the file: 466
    You should close the file: 467
    You should close the file: 468
    You should close the file: 469
    You should close the file: 470
    You should close the file: 471
    You should close the file: 472
    You should close the file: 473
    You should close the file: 474
    You should close the file: 475
    You should close the file: 476
    You should close the file: 477
    You should close the file: 478
    You should close the file: 479
    You should close the file: 480
    You should close the file: 481
    You should close the file: 482
    You should close the file: 483
    You should close the file: 484
    You should close the file: 485
    You should close the file: 486
    You should close the file: 487
    You should close the file: 488
    You should close the file: 489
    You should close the file: 490
    You should close the file: 491
    You should close the file: 492
    You should close the file: 493
    You should close the file: 494
    You should close the file: 495
    You should close the file: 496
    You should close the file: 497
    You should close the file: 498
    You should close the file: 499
    You should close the file: 500
    You should close the file: 501
    You should close the file: 502
    You should close the file: 503
    You should close the file: 504
    You should close the file: 505
    You should close the file: 506
    You should close the file: 507
    You should close the file: 508
    You should close the file: 509
    You should close the file: 510
    You should close the file: 511
    You should close the file: 512
    You should close the file: 513
    You should close the file: 514
    You should close the file: 515
    You should close the file: 516
    You should close the file: 517
    You should close the file: 518
    You should close the file: 519
    You should close the file: 520
    You should close the file: 521
    You should close the file: 522
    You should close the file: 523
    You should close the file: 524
    You should close the file: 525
    You should close the file: 526
    You should close the file: 527
    You should close the file: 528
    You should close the file: 529
    You should close the file: 530
    You should close the file: 531
    You should close the file: 532
    You should close the file: 533
    You should close the file: 534
    You should close the file: 535
    You should close the file: 536
    You should close the file: 537
    You should close the file: 538
    You should close the file: 539
    You should close the file: 540
    You should close the file: 541
    You should close the file: 542
    You should close the file: 543
    You should close the file: 544
    You should close the file: 545
    You should close the file: 546
    You should close the file: 547
    You should close the file: 548
    You should close the file: 549
    You should close the file: 550
    You should close the file: 551
    You should close the file: 552
    You should close the file: 553
    You should close the file: 554
    You should close the file: 555
    You should close the file: 556
    You should close the file: 557
    You should close the file: 558
    You should close the file: 559
    You should close the file: 560
    You should close the file: 561
    You should close the file: 562
    You should close the file: 563
    You should close the file: 564
    You should close the file: 565
    You should close the file: 566
    You should close the file: 567
    You should close the file: 568
    You should close the file: 569
    You should close the file: 570
    You should close the file: 571
    You should close the file: 572
    You should close the file: 573
    You should close the file: 574
    You should close the file: 575
    You should close the file: 576
    You should close the file: 577
    You should close the file: 578
    You should close the file: 579
    You should close the file: 580
    You should close the file: 581
    You should close the file: 582
    You should close the file: 583
    You should close the file: 584
    You should close the file: 585
    You should close the file: 586
    You should close the file: 587
    You should close the file: 588
    You should close the file: 589
    You should close the file: 590
    You should close the file: 591
    You should close the file: 592
    You should close the file: 593
    You should close the file: 594
    You should close the file: 595
    You should close the file: 596
    You should close the file: 597
    You should close the file: 598
    You should close the file: 599
    You should close the file: 600
    You should close the file: 601
    You should close the file: 602
    You should close the file: 603
    You should close the file: 604
    You should close the file: 605
    You should close the file: 606
    You should close the file: 607
    You should close the file: 608
    You should close the file: 609
    You should close the file: 610
    You should close the file: 611
    You should close the file: 612
    You should close the file: 613
    You should close the file: 614
    You should close the file: 615
    You should close the file: 616
    You should close the file: 617
    You should close the file: 618
    You should close the file: 619
    You should close the file: 620
    You should close the file: 621
    You should close the file: 622
    You should close the file: 623
    You should close the file: 624
    You should close the file: 625
    You should close the file: 626
    You should close the file: 627
    You should close the file: 628
    You should close the file: 629
    You should close the file: 630
    You should close the file: 631
    You should close the file: 632
    You should close the file: 633
    You should close the file: 634
    You should close the file: 635
    You should close the file: 636
    You should close the file: 637
    You should close the file: 638
    You should close the file: 639
    You should close the file: 640
    You should close the file: 641
    You should close the file: 642
    You should close the file: 643
    You should close the file: 644
    You should close the file: 645
    You should close the file: 646
    You should close the file: 647
    You should close the file: 648
    You should close the file: 649
    You should close the file: 650
    You should close the file: 651
    You should close the file: 652
    You should close the file: 653
    You should close the file: 654
    You should close the file: 655
    You should close the file: 656
    You should close the file: 657
    You should close the file: 658
    You should close the file: 659
    You should close the file: 660
    You should close the file: 661
    You should close the file: 662
    You should close the file: 663
    You should close the file: 664
    You should close the file: 665
    You should close the file: 666
    You should close the file: 667
    You should close the file: 668
    You should close the file: 669
    You should close the file: 670
    You should close the file: 671
    You should close the file: 672
    You should close the file: 673
    You should close the file: 674
    You should close the file: 675
    You should close the file: 676
    You should close the file: 677
    You should close the file: 678
    You should close the file: 679
    You should close the file: 680
    You should close the file: 681
    You should close the file: 682
    You should close the file: 683
    You should close the file: 684
    You should close the file: 685
    You should close the file: 686
    You should close the file: 687
    You should close the file: 688
    You should close the file: 689
    You should close the file: 690
    You should close the file: 691
    You should close the file: 692
    You should close the file: 693
    You should close the file: 694
    You should close the file: 695
    You should close the file: 696
    You should close the file: 697
    You should close the file: 698
    You should close the file: 699
    You should close the file: 700
    You should close the file: 701
    You should close the file: 702
    You should close the file: 703
    You should close the file: 704
    You should close the file: 705
    You should close the file: 706
    You should close the file: 707
    You should close the file: 708
    You should close the file: 709
    You should close the file: 710
    You should close the file: 711
    You should close the file: 712
    You should close the file: 713
    You should close the file: 714
    You should close the file: 715
    You should close the file: 716
    You should close the file: 717
    You should close the file: 718
    You should close the file: 719
    You should close the file: 720
    You should close the file: 721
    You should close the file: 722
    You should close the file: 723
    You should close the file: 724
    You should close the file: 725
    You should close the file: 726
    You should close the file: 727
    You should close the file: 728
    You should close the file: 729
    You should close the file: 730
    You should close the file: 731
    You should close the file: 732
    You should close the file: 733
    You should close the file: 734
    You should close the file: 735
    You should close the file: 736
    You should close the file: 737
    You should close the file: 738
    You should close the file: 739
    You should close the file: 740
    You should close the file: 741
    You should close the file: 742
    You should close the file: 743
    You should close the file: 744
    You should close the file: 745
    You should close the file: 746
    You should close the file: 747
    You should close the file: 748
    You should close the file: 749
    You should close the file: 750
    You should close the file: 751
    You should close the file: 752
    You should close the file: 753
    You should close the file: 754
    You should close the file: 755
    You should close the file: 756
    You should close the file: 757
    You should close the file: 758
    You should close the file: 759
    You should close the file: 760
    You should close the file: 761
    You should close the file: 762
    You should close the file: 763
    You should close the file: 764
    You should close the file: 765
    You should close the file: 766
    You should close the file: 767
    You should close the file: 768
    You should close the file: 769
    You should close the file: 770
    You should close the file: 771
    You should close the file: 772
    You should close the file: 773
    You should close the file: 774
    You should close the file: 775
    You should close the file: 776
    You should close the file: 777
    You should close the file: 778
    You should close the file: 779
    You should close the file: 780
    You should close the file: 781
    You should close the file: 782
    You should close the file: 783
    You should close the file: 784
    You should close the file: 785
    You should close the file: 786
    You should close the file: 787
    You should close the file: 788
    You should close the file: 789
    You should close the file: 790
    You should close the file: 791
    You should close the file: 792
    You should close the file: 793
    You should close the file: 794
    You should close the file: 795
    You should close the file: 796
    You should close the file: 797
    
    


```python
import os
os.remove('newfile.txt')
```

出现异常时的读写：


```python
f = open('newfile.txt','w')
for i in range(3000):
    x = 1.0 / (i - 1000)
    f.write('hello world: ' + str(i) + '\n')
```


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-25-8dc1cc9b29ec> in <module>()
          1 f = open('newfile.txt','w')
          2 for i in range(3000):
    ----> 3     x = 1.0 / (i - 1000)
          4     f.write('hello world: ' + str(i) + '\n')
    

    ZeroDivisionError: float division by zero



```python
g = open('newfile.txt', 'r')
print(g.read())
g.close()
```

    hello world: 0
    hello world: 1
    hello world: 2
    hello world: 3
    hello world: 4
    hello world: 5
    hello world: 6
    hello world: 7
    hello world: 8
    hello world: 9
    hello world: 10
    hello world: 11
    hello world: 12
    hello world: 13
    hello world: 14
    hello world: 15
    hello world: 16
    hello world: 17
    hello world: 18
    hello world: 19
    hello world: 20
    hello world: 21
    hello world: 22
    hello world: 23
    hello world: 24
    hello world: 25
    hello world: 26
    hello world: 27
    hello world: 28
    hello world: 29
    hello world: 30
    hello world: 31
    hello world: 32
    hello world: 33
    hello world: 34
    hello world: 35
    hello world: 36
    hello world: 37
    hello world: 38
    hello world: 39
    hello world: 40
    hello world: 41
    hello world: 42
    hello world: 43
    hello world: 44
    hello world: 45
    hello world: 46
    hello world: 47
    hello world: 48
    hello world: 49
    hello world: 50
    hello world: 51
    hello world: 52
    hello world: 53
    hello world: 54
    hello world: 55
    hello world: 56
    hello world: 57
    hello world: 58
    hello world: 59
    hello world: 60
    hello world: 61
    hello world: 62
    hello world: 63
    hello world: 64
    hello world: 65
    hello world: 66
    hello world: 67
    hello world: 68
    hello world: 69
    hello world: 70
    hello world: 71
    hello world: 72
    hello world: 73
    hello world: 74
    hello world: 75
    hello world: 76
    hello world: 77
    hello world: 78
    hello world: 79
    hello world: 80
    hello world: 81
    hello world: 82
    hello world: 83
    hello world: 84
    hello world: 85
    hello world: 86
    hello world: 87
    hello world: 88
    hello world: 89
    hello world: 90
    hello world: 91
    hello world: 92
    hello world: 93
    hello world: 94
    hello world: 95
    hello world: 96
    hello world: 97
    hello world: 98
    hello world: 99
    hello world: 100
    hello world: 101
    hello world: 102
    hello world: 103
    hello world: 104
    hello world: 105
    hello world: 106
    hello world: 107
    hello world: 108
    hello world: 109
    hello world: 110
    hello world: 111
    hello world: 112
    hello world: 113
    hello world: 114
    hello world: 115
    hello world: 116
    hello world: 117
    hello world: 118
    hello world: 119
    hello world: 120
    hello world: 121
    hello world: 122
    hello world: 123
    hello world: 124
    hello world: 125
    hello world: 126
    hello world: 127
    hello world: 128
    hello world: 129
    hello world: 130
    hello world: 131
    hello world: 132
    hello world: 133
    hello world: 134
    hello world: 135
    hello world: 136
    hello world: 137
    hello world: 138
    hello world: 139
    hello world: 140
    hello world: 141
    hello world: 142
    hello world: 143
    hello world: 144
    hello world: 145
    hello world: 146
    hello world: 147
    hello world: 148
    hello world: 149
    hello world: 150
    hello world: 151
    hello world: 152
    hello world: 153
    hello world: 154
    hello world: 155
    hello world: 156
    hello world: 157
    hello world: 158
    hello world: 159
    hello world: 160
    hello world: 161
    hello world: 162
    hello world: 163
    hello world: 164
    hello world: 165
    hello world: 166
    hello world: 167
    hello world: 168
    hello world: 169
    hello world: 170
    hello world: 171
    hello world: 172
    hello world: 173
    hello world: 174
    hello world: 175
    hello world: 176
    hello world: 177
    hello world: 178
    hello world: 179
    hello world: 180
    hello world: 181
    hello world: 182
    hello world: 183
    hello world: 184
    hello world: 185
    hello world: 186
    hello world: 187
    hello world: 188
    hello world: 189
    hello world: 190
    hello world: 191
    hello world: 192
    hello world: 193
    hello world: 194
    hello world: 195
    hello world: 196
    hello world: 197
    hello world: 198
    hello world: 199
    hello world: 200
    hello world: 201
    hello world: 202
    hello world: 203
    hello world: 204
    hello world: 205
    hello world: 206
    hello world: 207
    hello world: 208
    hello world: 209
    hello world: 210
    hello world: 211
    hello world: 212
    hello world: 213
    hello world: 214
    hello world: 215
    hello world: 216
    hello world: 217
    hello world: 218
    hello world: 219
    hello world: 220
    hello world: 221
    hello world: 222
    hello world: 223
    hello world: 224
    hello world: 225
    hello world: 226
    hello world: 227
    hello world: 228
    hello world: 229
    hello world: 230
    hello world: 231
    hello world: 232
    hello world: 233
    hello world: 234
    hello world: 235
    hello world: 236
    hello world: 237
    hello world: 238
    hello world: 239
    hello world: 240
    hello world: 241
    hello world: 242
    hello world: 243
    hello world: 244
    hello world: 245
    hello world: 246
    hello world: 247
    hello world: 248
    hello world: 249
    hello world: 250
    hello world: 251
    hello world: 252
    hello world: 253
    hello world: 254
    hello world: 255
    hello world: 256
    hello world: 257
    hello world: 258
    hello world: 259
    hello world: 260
    hello world: 261
    hello world: 262
    hello world: 263
    hello world: 264
    hello world: 265
    hello world: 266
    hello world: 267
    hello world: 268
    hello world: 269
    hello world: 270
    hello world: 271
    hello world: 272
    hello world: 273
    hello world: 274
    hello world: 275
    hello world: 276
    hello world: 277
    hello world: 278
    hello world: 279
    hello world: 280
    hello world: 281
    hello world: 282
    hello world: 283
    hello world: 284
    hello world: 285
    hello world: 286
    hello world: 287
    hello world: 288
    hello world: 289
    hello world: 290
    hello world: 291
    hello world: 292
    hello world: 293
    hello world: 294
    hello world: 295
    hello world: 296
    hello world: 297
    hello world: 298
    hello world: 299
    hello world: 300
    hello world: 301
    hello world: 302
    hello world: 303
    hello world: 304
    hello world: 305
    hello world: 306
    hello world: 307
    hello world: 308
    hello world: 309
    hello world: 310
    hello world: 311
    hello world: 312
    hello world: 313
    hello world: 314
    hello world: 315
    hello world: 316
    hello world: 317
    hello world: 318
    hello world: 319
    hello world: 320
    hello world: 321
    hello world: 322
    hello world: 323
    hello world: 324
    hello world: 325
    hello world: 326
    hello world: 327
    hello world: 328
    hello world: 329
    hello world: 330
    hello world: 331
    hello world: 332
    hello world: 333
    hello world: 334
    hello world: 335
    hello world: 336
    hello world: 337
    hello world: 338
    hello world: 339
    hello world: 340
    hello world: 341
    hello world: 342
    hello world: 343
    hello world: 344
    hello world: 345
    hello world: 346
    hello world: 347
    hello world: 348
    hello world: 349
    hello world: 350
    hello world: 351
    hello world: 352
    hello world: 353
    hello world: 354
    hello world: 355
    hello world: 356
    hello world: 357
    hello world: 358
    hello world: 359
    hello world: 360
    hello world: 361
    hello world: 362
    hello world: 363
    hello world: 364
    hello world: 365
    hello world: 366
    hello world: 367
    hello world: 368
    hello world: 369
    hello world: 370
    hello world: 371
    hello world: 372
    hello world: 373
    hello world: 374
    hello world: 375
    hello world: 376
    hello world: 377
    hello world: 378
    hello world: 379
    hello world: 380
    hello world: 381
    hello world: 382
    hello world: 383
    hello world: 384
    hello world: 385
    hello world: 386
    hello world: 387
    hello world: 388
    hello world: 389
    hello world: 390
    hello world: 391
    hello world: 392
    hello world: 393
    hello world: 394
    hello world: 395
    hello world: 396
    hello world: 397
    hello world: 398
    hello world: 399
    hello world: 400
    hello world: 401
    hello world: 402
    hello world: 403
    hello world: 404
    hello world: 405
    hello world: 406
    hello world: 407
    hello world: 408
    hello world: 409
    hello world: 410
    hello world: 411
    hello world: 412
    hello world: 413
    hello world: 414
    hello world: 415
    hello world: 416
    hello world: 417
    hello world: 418
    hello world: 419
    hello world: 420
    hello world: 421
    hello world: 422
    hello world: 423
    hello world: 424
    hello world: 425
    hello world: 426
    hello world: 427
    hello world: 428
    hello world: 429
    hello world: 430
    hello world: 431
    hello world: 432
    hello world: 433
    hello world: 434
    hello world: 435
    hello world: 436
    hello world: 437
    hello world: 438
    hello world: 439
    hello world: 440
    hello world: 441
    hello world: 442
    hello world: 443
    hello world: 444
    hello world: 445
    hello world: 446
    hello world: 447
    hello world: 448
    hello world: 449
    hello world: 450
    hello world: 451
    hello world: 452
    hello world: 453
    hello world: 454
    hello world: 455
    hello world: 456
    hello world: 457
    hello world: 458
    hello world: 459
    hello world: 460
    hello world: 461
    hello world: 462
    hello world: 463
    hello world: 464
    hello world: 465
    hello world: 466
    hello world: 467
    hello world: 468
    hello world: 469
    hello world: 470
    hello world: 471
    hello world: 472
    hello world: 473
    hello world: 474
    hello world: 475
    hello world: 476
    hello world: 477
    hello world: 478
    hello world: 479
    hello world: 480
    hello world: 481
    hello world: 482
    hello world: 483
    hello world: 484
    hello world: 485
    hello world: 486
    hello world: 487
    hello world: 488
    hello world: 489
    hello world: 490
    hello world: 491
    hello world: 492
    hello world: 493
    hello world: 494
    hello world: 495
    hello world: 496
    hello world: 497
    hello world: 498
    hello world: 499
    hello world: 500
    hello world: 501
    hello world: 502
    hello world: 503
    hello world: 504
    hello world: 505
    hello world: 506
    hello world: 507
    hello world: 508
    hello world: 509
    hello world: 510
    hello world: 511
    hello world: 512
    hello world: 513
    hello world: 514
    hello world: 515
    hello world: 516
    hello world: 517
    hello world: 518
    hello world: 519
    hello world: 520
    hello world: 521
    hello world: 522
    hello world: 523
    hello world: 524
    hello world: 525
    hello world: 526
    hello world: 527
    hello world: 528
    hello world: 529
    hello world: 530
    hello world: 531
    hello world: 532
    hello world: 533
    hello world: 534
    hello world: 535
    hello world: 536
    hello world: 537
    hello world: 538
    hello world: 539
    hello world: 540
    hello world: 541
    hello world: 542
    hello world: 543
    hello world: 544
    hello world: 545
    hello world: 546
    hello world: 547
    hello world: 548
    hello world: 549
    hello world: 550
    hello world: 551
    hello world: 552
    hello world: 553
    hello world: 554
    hello world: 555
    hello world: 556
    hello world: 557
    hello world: 558
    hello world: 559
    hello world: 560
    hello world: 561
    hello world: 562
    hello world: 563
    hello world: 564
    hello world: 565
    hello world: 566
    hello world: 567
    hello world: 568
    hello world: 569
    hello world: 570
    hello world: 571
    hello world: 572
    hello world: 573
    hello world: 574
    hello world: 575
    hello world: 576
    hello world: 577
    hello world: 578
    hello world: 579
    hello world: 580
    hello world: 581
    hello world: 582
    hello world: 583
    hello world: 584
    hello world: 585
    hello world: 586
    hello world: 587
    hello world: 588
    hello world: 589
    hello world: 590
    hello world: 591
    hello world: 592
    hello world: 593
    hello world: 594
    hello world: 595
    hello world: 596
    hello world: 597
    hello world: 598
    hello world: 599
    hello world: 600
    hello world: 601
    hello world: 602
    hello world: 603
    hello world: 604
    hello world: 605
    hello world: 606
    hello world: 607
    hello world: 608
    hello world: 609
    hello world: 610
    hello world: 611
    hello world: 612
    hello world: 613
    hello world: 614
    hello world: 615
    hello world: 616
    hello world: 617
    hello world: 618
    hello world: 619
    hello world: 620
    hello world: 621
    hello world: 622
    hello world: 623
    hello world: 624
    hello world: 625
    hello world: 626
    hello world: 627
    hello world: 628
    hello world: 629
    hello world: 630
    hello world: 631
    hello world: 632
    hello world: 633
    hello world: 634
    hello world: 635
    hello world: 636
    hello world: 637
    hello world: 638
    hello world: 639
    hello world: 640
    hello world: 641
    hello world: 642
    hello world: 643
    hello world: 644
    hello world: 645
    hello world: 646
    hello world: 647
    hello world: 648
    hello world: 649
    hello world: 650
    hello world: 651
    hello world: 652
    hello world: 653
    hello world: 654
    hello world: 655
    hello world: 656
    hello world: 657
    hello world: 658
    hello world: 659
    hello world: 660
    hello world: 661
    hello world: 662
    hello world: 663
    hello world: 664
    hello world: 665
    hello world: 666
    hello world: 667
    hello world: 668
    hello world: 669
    hello world: 670
    hello world: 671
    hello world: 672
    hello world: 673
    hello world: 674
    hello world: 675
    hello world: 676
    hello world: 677
    hello world: 678
    hello world: 679
    hello world: 680
    hello world: 681
    hello world: 682
    hello world: 683
    hello world: 684
    hello world: 685
    hello world: 686
    hello world: 687
    hello world: 688
    hello world: 689
    hello world: 690
    hello world: 691
    hello world: 692
    hello world: 693
    hello world: 694
    hello world: 695
    hello world: 696
    hello world: 697
    hello world: 698
    hello world: 699
    hello world: 700
    hello world: 701
    hello world: 702
    hello world: 703
    hello world: 704
    hello world: 705
    hello world: 706
    hello world: 707
    hello world: 708
    hello world: 709
    hello world: 710
    hello world: 711
    hello world: 712
    hello world: 713
    hello world: 714
    hello world: 715
    hello world: 716
    hello world: 717
    hello world: 718
    hello world: 719
    hello world: 720
    hello world: 721
    hello world: 722
    hello world: 723
    hello world: 724
    hello world: 725
    hello world: 726
    hello world: 727
    hello world: 728
    hello world: 729
    hello world: 730
    hello world: 731
    hello world: 732
    hello world: 733
    hello world: 734
    hello world: 735
    hello world: 736
    hello world: 737
    hello world: 738
    hello world: 739
    hello world: 740
    hello world: 741
    hello world: 742
    hello world: 743
    hello world: 744
    hello world: 745
    hello world: 746
    hello world: 747
    hello world: 748
    hello world: 749
    hello world: 750
    hello world: 751
    hello world: 752
    hello world: 753
    hello world: 754
    hello world: 755
    hello world: 756
    hello world: 757
    hello world: 758
    hello world: 759
    hello world: 760
    hello world: 761
    hello world: 762
    hello world: 763
    hello world: 764
    hello world: 765
    hello world: 766
    hello world: 767
    hello world: 768
    hello world: 769
    hello world: 770
    hello world: 771
    hello world: 772
    hello world: 773
    hello world: 774
    hello world: 775
    hello world: 776
    hello world: 777
    hello world: 778
    hello world: 779
    hello world: 780
    hello world: 781
    hello world: 782
    hello world: 783
    hello world: 784
    hello world: 785
    hello world: 786
    hello world: 787
    hello world: 788
    hello world: 789
    hello world: 790
    hello world: 791
    hello world: 792
    hello world: 793
    hello world: 794
    hello world: 795
    hello world: 796
    hello world: 797
    hello world: 798
    hello world: 799
    hello world: 800
    hello world: 801
    hello world: 802
    hello world: 803
    hello world: 804
    hello world: 805
    hello world: 806
    hello world: 807
    hello world: 808
    hello world: 809
    hello world: 810
    hello world: 811
    hello world: 812
    hello world: 813
    hello world: 814
    hello world: 815
    hello world: 816
    hello world: 817
    hello world: 818
    hello world: 819
    hello world: 820
    hello world: 821
    hello world: 822
    hello world: 823
    hello world: 824
    hello world: 825
    hello world: 826
    hello world: 827
    hello world: 828
    hello world: 829
    hello world: 830
    hello world: 831
    hello world: 832
    hello world: 833
    hello world: 834
    hello world: 835
    hello world: 836
    hello world: 837
    hello world: 838
    hello world: 839
    hello world: 840
    hello world: 841
    hello world: 842
    hello world: 843
    hello world: 844
    hello world: 845
    hello world: 846
    hello world: 847
    hello world: 848
    hello world: 849
    hello world: 850
    hello world: 851
    hello world: 852
    hello world: 853
    hello world: 854
    hello world: 855
    hello world: 856
    hello world: 857
    hello world: 858
    hello world: 859
    hello world: 860
    hello world: 861
    hello world: 862
    hello world: 863
    hello world: 864
    hello world: 865
    hello world: 866
    hello world: 867
    hello world: 868
    hello world: 869
    hello world: 870
    hello world: 871
    hello world: 872
    hello world: 873
    hello world: 874
    hello world: 875
    hello world: 876
    hello world: 877
    hello world: 878
    hello world: 879
    hello world: 880
    hello world: 881
    hello world: 882
    hello world: 883
    hello world: 884
    hello world: 885
    hello world: 886
    hello world: 887
    hello world: 888
    hello world: 889
    hello world: 890
    hello world: 891
    hello world: 892
    hello world: 893
    hello world: 894
    hello world: 895
    hello world: 896
    hello world: 897
    hello world: 898
    hello world: 899
    hello world: 900
    hello world: 901
    hello world: 902
    hello world: 903
    hello world: 904
    hello world: 905
    hello world: 906
    hello world: 907
    hello world: 908
    hello world: 909
    hello world: 910
    hello world: 911
    hello world: 912
    hello world: 913
    hello world: 914
    hello world: 915
    hello world: 916
    hello world: 917
    hello world: 918
    hello world: 919
    hello world: 920
    hello world: 921
    hello world: 922
    hello world: 923
    hello world: 924
    hello world: 925
    hello world: 926
    hello world: 927
    hello world: 928
    hello world: 929
    hello world: 930
    hello world: 931
    hello world: 932
    hello world: 933
    hello world: 934
    hello world: 935
    hello world: 936
    hello world: 937
    hello world: 938
    hello world: 939
    hello world: 940
    hello world: 941
    hello world: 942
    hello world: 943
    hello world: 944
    hello world: 945
    hello world: 946
    hello world: 947
    hello world: 948
    hello world: 949
    hello world: 950
    hello world: 951
    hello world: 952
    hello world: 953
    hello world: 954
    hello world: 955
    hello world: 956
    hello world: 957
    hello world: 958
    hello world: 959
    hello world: 960
    hello world: 961
    hello world: 962
    hello world: 963
    hello world: 964
    hello world: 965
    hello world: 966
    hello world: 967
    hello world: 968
    hello world: 969
    hello world: 970
    
    

## with方法  
事实上，Python提供了一个安全的方法，当 `with` 代码块的内容结束后，Python会自动调用它的 `close` 方法，确保读写的安全：


```python
with open('newfile.txt','w') as f:
    for i in range(3000):
        x = 1.0 / (i - 1000)
        f.write('hello world: ' + str(i) + '\n')
```


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-28-9d2a70065b27> in <module>()
          1 with open('newfile.txt','w') as f:
          2     for i in range(3000):
    ----> 3         x = 1.0 / (i - 1000)
          4         f.write('hello world: ' + str(i) + '\n')
    

    ZeroDivisionError: float division by zero



```python
g = open('newfile.txt', 'r')
print(g.read())
g.close()
```

    hello world: 0
    hello world: 1
    hello world: 2
    hello world: 3
    hello world: 4
    hello world: 5
    hello world: 6
    hello world: 7
    hello world: 8
    hello world: 9
    hello world: 10
    hello world: 11
    hello world: 12
    hello world: 13
    hello world: 14
    hello world: 15
    hello world: 16
    hello world: 17
    hello world: 18
    hello world: 19
    hello world: 20
    hello world: 21
    hello world: 22
    hello world: 23
    hello world: 24
    hello world: 25
    hello world: 26
    hello world: 27
    hello world: 28
    hello world: 29
    hello world: 30
    hello world: 31
    hello world: 32
    hello world: 33
    hello world: 34
    hello world: 35
    hello world: 36
    hello world: 37
    hello world: 38
    hello world: 39
    hello world: 40
    hello world: 41
    hello world: 42
    hello world: 43
    hello world: 44
    hello world: 45
    hello world: 46
    hello world: 47
    hello world: 48
    hello world: 49
    hello world: 50
    hello world: 51
    hello world: 52
    hello world: 53
    hello world: 54
    hello world: 55
    hello world: 56
    hello world: 57
    hello world: 58
    hello world: 59
    hello world: 60
    hello world: 61
    hello world: 62
    hello world: 63
    hello world: 64
    hello world: 65
    hello world: 66
    hello world: 67
    hello world: 68
    hello world: 69
    hello world: 70
    hello world: 71
    hello world: 72
    hello world: 73
    hello world: 74
    hello world: 75
    hello world: 76
    hello world: 77
    hello world: 78
    hello world: 79
    hello world: 80
    hello world: 81
    hello world: 82
    hello world: 83
    hello world: 84
    hello world: 85
    hello world: 86
    hello world: 87
    hello world: 88
    hello world: 89
    hello world: 90
    hello world: 91
    hello world: 92
    hello world: 93
    hello world: 94
    hello world: 95
    hello world: 96
    hello world: 97
    hello world: 98
    hello world: 99
    hello world: 100
    hello world: 101
    hello world: 102
    hello world: 103
    hello world: 104
    hello world: 105
    hello world: 106
    hello world: 107
    hello world: 108
    hello world: 109
    hello world: 110
    hello world: 111
    hello world: 112
    hello world: 113
    hello world: 114
    hello world: 115
    hello world: 116
    hello world: 117
    hello world: 118
    hello world: 119
    hello world: 120
    hello world: 121
    hello world: 122
    hello world: 123
    hello world: 124
    hello world: 125
    hello world: 126
    hello world: 127
    hello world: 128
    hello world: 129
    hello world: 130
    hello world: 131
    hello world: 132
    hello world: 133
    hello world: 134
    hello world: 135
    hello world: 136
    hello world: 137
    hello world: 138
    hello world: 139
    hello world: 140
    hello world: 141
    hello world: 142
    hello world: 143
    hello world: 144
    hello world: 145
    hello world: 146
    hello world: 147
    hello world: 148
    hello world: 149
    hello world: 150
    hello world: 151
    hello world: 152
    hello world: 153
    hello world: 154
    hello world: 155
    hello world: 156
    hello world: 157
    hello world: 158
    hello world: 159
    hello world: 160
    hello world: 161
    hello world: 162
    hello world: 163
    hello world: 164
    hello world: 165
    hello world: 166
    hello world: 167
    hello world: 168
    hello world: 169
    hello world: 170
    hello world: 171
    hello world: 172
    hello world: 173
    hello world: 174
    hello world: 175
    hello world: 176
    hello world: 177
    hello world: 178
    hello world: 179
    hello world: 180
    hello world: 181
    hello world: 182
    hello world: 183
    hello world: 184
    hello world: 185
    hello world: 186
    hello world: 187
    hello world: 188
    hello world: 189
    hello world: 190
    hello world: 191
    hello world: 192
    hello world: 193
    hello world: 194
    hello world: 195
    hello world: 196
    hello world: 197
    hello world: 198
    hello world: 199
    hello world: 200
    hello world: 201
    hello world: 202
    hello world: 203
    hello world: 204
    hello world: 205
    hello world: 206
    hello world: 207
    hello world: 208
    hello world: 209
    hello world: 210
    hello world: 211
    hello world: 212
    hello world: 213
    hello world: 214
    hello world: 215
    hello world: 216
    hello world: 217
    hello world: 218
    hello world: 219
    hello world: 220
    hello world: 221
    hello world: 222
    hello world: 223
    hello world: 224
    hello world: 225
    hello world: 226
    hello world: 227
    hello world: 228
    hello world: 229
    hello world: 230
    hello world: 231
    hello world: 232
    hello world: 233
    hello world: 234
    hello world: 235
    hello world: 236
    hello world: 237
    hello world: 238
    hello world: 239
    hello world: 240
    hello world: 241
    hello world: 242
    hello world: 243
    hello world: 244
    hello world: 245
    hello world: 246
    hello world: 247
    hello world: 248
    hello world: 249
    hello world: 250
    hello world: 251
    hello world: 252
    hello world: 253
    hello world: 254
    hello world: 255
    hello world: 256
    hello world: 257
    hello world: 258
    hello world: 259
    hello world: 260
    hello world: 261
    hello world: 262
    hello world: 263
    hello world: 264
    hello world: 265
    hello world: 266
    hello world: 267
    hello world: 268
    hello world: 269
    hello world: 270
    hello world: 271
    hello world: 272
    hello world: 273
    hello world: 274
    hello world: 275
    hello world: 276
    hello world: 277
    hello world: 278
    hello world: 279
    hello world: 280
    hello world: 281
    hello world: 282
    hello world: 283
    hello world: 284
    hello world: 285
    hello world: 286
    hello world: 287
    hello world: 288
    hello world: 289
    hello world: 290
    hello world: 291
    hello world: 292
    hello world: 293
    hello world: 294
    hello world: 295
    hello world: 296
    hello world: 297
    hello world: 298
    hello world: 299
    hello world: 300
    hello world: 301
    hello world: 302
    hello world: 303
    hello world: 304
    hello world: 305
    hello world: 306
    hello world: 307
    hello world: 308
    hello world: 309
    hello world: 310
    hello world: 311
    hello world: 312
    hello world: 313
    hello world: 314
    hello world: 315
    hello world: 316
    hello world: 317
    hello world: 318
    hello world: 319
    hello world: 320
    hello world: 321
    hello world: 322
    hello world: 323
    hello world: 324
    hello world: 325
    hello world: 326
    hello world: 327
    hello world: 328
    hello world: 329
    hello world: 330
    hello world: 331
    hello world: 332
    hello world: 333
    hello world: 334
    hello world: 335
    hello world: 336
    hello world: 337
    hello world: 338
    hello world: 339
    hello world: 340
    hello world: 341
    hello world: 342
    hello world: 343
    hello world: 344
    hello world: 345
    hello world: 346
    hello world: 347
    hello world: 348
    hello world: 349
    hello world: 350
    hello world: 351
    hello world: 352
    hello world: 353
    hello world: 354
    hello world: 355
    hello world: 356
    hello world: 357
    hello world: 358
    hello world: 359
    hello world: 360
    hello world: 361
    hello world: 362
    hello world: 363
    hello world: 364
    hello world: 365
    hello world: 366
    hello world: 367
    hello world: 368
    hello world: 369
    hello world: 370
    hello world: 371
    hello world: 372
    hello world: 373
    hello world: 374
    hello world: 375
    hello world: 376
    hello world: 377
    hello world: 378
    hello world: 379
    hello world: 380
    hello world: 381
    hello world: 382
    hello world: 383
    hello world: 384
    hello world: 385
    hello world: 386
    hello world: 387
    hello world: 388
    hello world: 389
    hello world: 390
    hello world: 391
    hello world: 392
    hello world: 393
    hello world: 394
    hello world: 395
    hello world: 396
    hello world: 397
    hello world: 398
    hello world: 399
    hello world: 400
    hello world: 401
    hello world: 402
    hello world: 403
    hello world: 404
    hello world: 405
    hello world: 406
    hello world: 407
    hello world: 408
    hello world: 409
    hello world: 410
    hello world: 411
    hello world: 412
    hello world: 413
    hello world: 414
    hello world: 415
    hello world: 416
    hello world: 417
    hello world: 418
    hello world: 419
    hello world: 420
    hello world: 421
    hello world: 422
    hello world: 423
    hello world: 424
    hello world: 425
    hello world: 426
    hello world: 427
    hello world: 428
    hello world: 429
    hello world: 430
    hello world: 431
    hello world: 432
    hello world: 433
    hello world: 434
    hello world: 435
    hello world: 436
    hello world: 437
    hello world: 438
    hello world: 439
    hello world: 440
    hello world: 441
    hello world: 442
    hello world: 443
    hello world: 444
    hello world: 445
    hello world: 446
    hello world: 447
    hello world: 448
    hello world: 449
    hello world: 450
    hello world: 451
    hello world: 452
    hello world: 453
    hello world: 454
    hello world: 455
    hello world: 456
    hello world: 457
    hello world: 458
    hello world: 459
    hello world: 460
    hello world: 461
    hello world: 462
    hello world: 463
    hello world: 464
    hello world: 465
    hello world: 466
    hello world: 467
    hello world: 468
    hello world: 469
    hello world: 470
    hello world: 471
    hello world: 472
    hello world: 473
    hello world: 474
    hello world: 475
    hello world: 476
    hello world: 477
    hello world: 478
    hello world: 479
    hello world: 480
    hello world: 481
    hello world: 482
    hello world: 483
    hello world: 484
    hello world: 485
    hello world: 486
    hello world: 487
    hello world: 488
    hello world: 489
    hello world: 490
    hello world: 491
    hello world: 492
    hello world: 493
    hello world: 494
    hello world: 495
    hello world: 496
    hello world: 497
    hello world: 498
    hello world: 499
    hello world: 500
    hello world: 501
    hello world: 502
    hello world: 503
    hello world: 504
    hello world: 505
    hello world: 506
    hello world: 507
    hello world: 508
    hello world: 509
    hello world: 510
    hello world: 511
    hello world: 512
    hello world: 513
    hello world: 514
    hello world: 515
    hello world: 516
    hello world: 517
    hello world: 518
    hello world: 519
    hello world: 520
    hello world: 521
    hello world: 522
    hello world: 523
    hello world: 524
    hello world: 525
    hello world: 526
    hello world: 527
    hello world: 528
    hello world: 529
    hello world: 530
    hello world: 531
    hello world: 532
    hello world: 533
    hello world: 534
    hello world: 535
    hello world: 536
    hello world: 537
    hello world: 538
    hello world: 539
    hello world: 540
    hello world: 541
    hello world: 542
    hello world: 543
    hello world: 544
    hello world: 545
    hello world: 546
    hello world: 547
    hello world: 548
    hello world: 549
    hello world: 550
    hello world: 551
    hello world: 552
    hello world: 553
    hello world: 554
    hello world: 555
    hello world: 556
    hello world: 557
    hello world: 558
    hello world: 559
    hello world: 560
    hello world: 561
    hello world: 562
    hello world: 563
    hello world: 564
    hello world: 565
    hello world: 566
    hello world: 567
    hello world: 568
    hello world: 569
    hello world: 570
    hello world: 571
    hello world: 572
    hello world: 573
    hello world: 574
    hello world: 575
    hello world: 576
    hello world: 577
    hello world: 578
    hello world: 579
    hello world: 580
    hello world: 581
    hello world: 582
    hello world: 583
    hello world: 584
    hello world: 585
    hello world: 586
    hello world: 587
    hello world: 588
    hello world: 589
    hello world: 590
    hello world: 591
    hello world: 592
    hello world: 593
    hello world: 594
    hello world: 595
    hello world: 596
    hello world: 597
    hello world: 598
    hello world: 599
    hello world: 600
    hello world: 601
    hello world: 602
    hello world: 603
    hello world: 604
    hello world: 605
    hello world: 606
    hello world: 607
    hello world: 608
    hello world: 609
    hello world: 610
    hello world: 611
    hello world: 612
    hello world: 613
    hello world: 614
    hello world: 615
    hello world: 616
    hello world: 617
    hello world: 618
    hello world: 619
    hello world: 620
    hello world: 621
    hello world: 622
    hello world: 623
    hello world: 624
    hello world: 625
    hello world: 626
    hello world: 627
    hello world: 628
    hello world: 629
    hello world: 630
    hello world: 631
    hello world: 632
    hello world: 633
    hello world: 634
    hello world: 635
    hello world: 636
    hello world: 637
    hello world: 638
    hello world: 639
    hello world: 640
    hello world: 641
    hello world: 642
    hello world: 643
    hello world: 644
    hello world: 645
    hello world: 646
    hello world: 647
    hello world: 648
    hello world: 649
    hello world: 650
    hello world: 651
    hello world: 652
    hello world: 653
    hello world: 654
    hello world: 655
    hello world: 656
    hello world: 657
    hello world: 658
    hello world: 659
    hello world: 660
    hello world: 661
    hello world: 662
    hello world: 663
    hello world: 664
    hello world: 665
    hello world: 666
    hello world: 667
    hello world: 668
    hello world: 669
    hello world: 670
    hello world: 671
    hello world: 672
    hello world: 673
    hello world: 674
    hello world: 675
    hello world: 676
    hello world: 677
    hello world: 678
    hello world: 679
    hello world: 680
    hello world: 681
    hello world: 682
    hello world: 683
    hello world: 684
    hello world: 685
    hello world: 686
    hello world: 687
    hello world: 688
    hello world: 689
    hello world: 690
    hello world: 691
    hello world: 692
    hello world: 693
    hello world: 694
    hello world: 695
    hello world: 696
    hello world: 697
    hello world: 698
    hello world: 699
    hello world: 700
    hello world: 701
    hello world: 702
    hello world: 703
    hello world: 704
    hello world: 705
    hello world: 706
    hello world: 707
    hello world: 708
    hello world: 709
    hello world: 710
    hello world: 711
    hello world: 712
    hello world: 713
    hello world: 714
    hello world: 715
    hello world: 716
    hello world: 717
    hello world: 718
    hello world: 719
    hello world: 720
    hello world: 721
    hello world: 722
    hello world: 723
    hello world: 724
    hello world: 725
    hello world: 726
    hello world: 727
    hello world: 728
    hello world: 729
    hello world: 730
    hello world: 731
    hello world: 732
    hello world: 733
    hello world: 734
    hello world: 735
    hello world: 736
    hello world: 737
    hello world: 738
    hello world: 739
    hello world: 740
    hello world: 741
    hello world: 742
    hello world: 743
    hello world: 744
    hello world: 745
    hello world: 746
    hello world: 747
    hello world: 748
    hello world: 749
    hello world: 750
    hello world: 751
    hello world: 752
    hello world: 753
    hello world: 754
    hello world: 755
    hello world: 756
    hello world: 757
    hello world: 758
    hello world: 759
    hello world: 760
    hello world: 761
    hello world: 762
    hello world: 763
    hello world: 764
    hello world: 765
    hello world: 766
    hello world: 767
    hello world: 768
    hello world: 769
    hello world: 770
    hello world: 771
    hello world: 772
    hello world: 773
    hello world: 774
    hello world: 775
    hello world: 776
    hello world: 777
    hello world: 778
    hello world: 779
    hello world: 780
    hello world: 781
    hello world: 782
    hello world: 783
    hello world: 784
    hello world: 785
    hello world: 786
    hello world: 787
    hello world: 788
    hello world: 789
    hello world: 790
    hello world: 791
    hello world: 792
    hello world: 793
    hello world: 794
    hello world: 795
    hello world: 796
    hello world: 797
    hello world: 798
    hello world: 799
    hello world: 800
    hello world: 801
    hello world: 802
    hello world: 803
    hello world: 804
    hello world: 805
    hello world: 806
    hello world: 807
    hello world: 808
    hello world: 809
    hello world: 810
    hello world: 811
    hello world: 812
    hello world: 813
    hello world: 814
    hello world: 815
    hello world: 816
    hello world: 817
    hello world: 818
    hello world: 819
    hello world: 820
    hello world: 821
    hello world: 822
    hello world: 823
    hello world: 824
    hello world: 825
    hello world: 826
    hello world: 827
    hello world: 828
    hello world: 829
    hello world: 830
    hello world: 831
    hello world: 832
    hello world: 833
    hello world: 834
    hello world: 835
    hello world: 836
    hello world: 837
    hello world: 838
    hello world: 839
    hello world: 840
    hello world: 841
    hello world: 842
    hello world: 843
    hello world: 844
    hello world: 845
    hello world: 846
    hello world: 847
    hello world: 848
    hello world: 849
    hello world: 850
    hello world: 851
    hello world: 852
    hello world: 853
    hello world: 854
    hello world: 855
    hello world: 856
    hello world: 857
    hello world: 858
    hello world: 859
    hello world: 860
    hello world: 861
    hello world: 862
    hello world: 863
    hello world: 864
    hello world: 865
    hello world: 866
    hello world: 867
    hello world: 868
    hello world: 869
    hello world: 870
    hello world: 871
    hello world: 872
    hello world: 873
    hello world: 874
    hello world: 875
    hello world: 876
    hello world: 877
    hello world: 878
    hello world: 879
    hello world: 880
    hello world: 881
    hello world: 882
    hello world: 883
    hello world: 884
    hello world: 885
    hello world: 886
    hello world: 887
    hello world: 888
    hello world: 889
    hello world: 890
    hello world: 891
    hello world: 892
    hello world: 893
    hello world: 894
    hello world: 895
    hello world: 896
    hello world: 897
    hello world: 898
    hello world: 899
    hello world: 900
    hello world: 901
    hello world: 902
    hello world: 903
    hello world: 904
    hello world: 905
    hello world: 906
    hello world: 907
    hello world: 908
    hello world: 909
    hello world: 910
    hello world: 911
    hello world: 912
    hello world: 913
    hello world: 914
    hello world: 915
    hello world: 916
    hello world: 917
    hello world: 918
    hello world: 919
    hello world: 920
    hello world: 921
    hello world: 922
    hello world: 923
    hello world: 924
    hello world: 925
    hello world: 926
    hello world: 927
    hello world: 928
    hello world: 929
    hello world: 930
    hello world: 931
    hello world: 932
    hello world: 933
    hello world: 934
    hello world: 935
    hello world: 936
    hello world: 937
    hello world: 938
    hello world: 939
    hello world: 940
    hello world: 941
    hello world: 942
    hello world: 943
    hello world: 944
    hello world: 945
    hello world: 946
    hello world: 947
    hello world: 948
    hello world: 949
    hello world: 950
    hello world: 951
    hello world: 952
    hello world: 953
    hello world: 954
    hello world: 955
    hello world: 956
    hello world: 957
    hello world: 958
    hello world: 959
    hello world: 960
    hello world: 961
    hello world: 962
    hello world: 963
    hello world: 964
    hello world: 965
    hello world: 966
    hello world: 967
    hello world: 968
    hello world: 969
    hello world: 970
    hello world: 971
    hello world: 972
    hello world: 973
    hello world: 974
    hello world: 975
    hello world: 976
    hello world: 977
    hello world: 978
    hello world: 979
    hello world: 980
    hello world: 981
    hello world: 982
    hello world: 983
    hello world: 984
    hello world: 985
    hello world: 986
    hello world: 987
    hello world: 988
    hello world: 989
    hello world: 990
    hello world: 991
    hello world: 992
    hello world: 993
    hello world: 994
    hello world: 995
    hello world: 996
    hello world: 997
    hello world: 998
    hello world: 999
    
    


```python
import os 
os.remove('newfile.txt')
```
