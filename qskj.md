         /**
         * 1.
         * +++ 写一个方法, 接受一个字符串，
         * 处理该字符串，
         * 将相同的字符集合在一起，
         * 然后返回新字符，
         * 先出现的字符集合应该排在前面
         * 如下这个例子：
         * 接受到：ddaeddceddbebca
         * 返回：  ddddddaaeeeccbb
         * @param {string} text
         * @returns {string}
         */
        function assembleChars(text) {
            const strLength = text.length;
            let str = text.slice();
            let resultStr = '';

            const obj = {}
            for (let i = 0; i < strLength; i++) {
                let char = str.charAt(i);
                if (obj[char]) {
                    obj[char]++;
                } else {
                    obj[char] = 1;
                }
            }

            Object.entries(obj).map(item => {
                const [str, nums] = item;
                for (let i = 0; i < nums; i++) {
                    resultStr += str;
                }
            })

            // while (str.length > 0) {
            // const v = str.substr(0, 1);//第一个值
            // if (v === lastStr) {
            //     const location = resultStr.lastIndexOf(lastStr);
            //     resultStr = resultStr.slice(0, location) + v + resultStr.slice(location)
            // } else {
            //     resultStr += v;
            // }
            // }
            return resultStr;
        }
        /**
        * 2.
         * +++ 写一个方法，
         * 接受一个下滑线分割的字符串，
         * 将其变成驼峰方式的字符串返回。
         * 如下这个例子：
         * 接受到：to_be_or_not_to_be 
         * 返回： toBeOrNotToBe
         * @param {string} text
         * @returns {string}
         */
        function lodashJoinToCamelCase(text) {
            const strLength = text.length;
            let array = text.split('_');
            let resultStr = '';
            for (let i = 0; i < array.length; i++) {
                const str = array[i];
                if (i === 0) {
                    resultStr += str;
                } else {
                    const upper = str[0].toUpperCase() + str.slice(1);
                    resultStr += upper;
                }

            }
            return resultStr;
        }
        /**
         * 3.
         * +++ 写一个方法，
         * 接受一个n*n整数二维数组(正方形矩阵)
         * 
         * 算出位于其对角线上所有整数之和，
         * 返回这个和
         * 
         * 不能更改传入的数组。
         * @param {number[][]} matrix
         * @returns {number}
         */
        function getSumOfNumbersOnSquareMatrixDiagonal(matrix) {
            let n = matrix.length;
            let sum1 = 0;
            let sum2 = 0;
            for (let i = 0; i < n; i++) {
                for (let j = 0; j < n; j++) {
                    // console.log(i, j, matrix[i][j]);
                    if (i === j) {
                        sum1 += matrix[i][j];
                    } else if (j === n - i - 1) {
                        sum2 += matrix[i][n - i - 1];
                    }
                }
            }
            // const location = Math.floor(n / 2);
            // const db = matrix[location][location];
            // console.log(sum1, sum2, db)
            return parseInt(sum1 + sum2);
        }


        /**
         * @typedef {Object} ICharCountItem
         * @property {string} char 字符
         * @property {number} count 该字符出现的次数
         * @property {percent} string 该数字占的百分比，字符串形式
         */

        /**
         * 4.
         * +++ 写一个方法，接受一个字符串；
         * 统计该字符串中各个字符出现的次数和概率，
         * 得到一个数组作为统计结果，返回该结果
         * 要求结果数组按字符出现次数
         * 从小到大的方式排好序
         * 数组中的每一项数据结构如下：
         * ```
         * {
         *    char: 'a',  // 是哪个字符
         *    count: 5，// 该字符出现的次数
         *    percent: '25%' 该数字占的百分比，字符串形式
         * }
         * ```
         * @param {string} text
         * @returns {ICharCountItem[]}
         */
        function countCharactors(text) {
            // let array = text.split('');
            const strLength = text.length;
            let str = text.slice();
            let resultArr = [];
            const obj = {}
            for (let i = 0; i < strLength; i++) {
                let char = str.charAt(i);
                if (obj[char]) {
                    obj[char]++;
                } else {
                    obj[char] = 1;
                }
            }
            for (const key in obj) {
                const count = obj[key];
                const percent = parseFloat((count / strLength) * 100).toFixed(2) + '%';
                resultArr.push({
                    char: key,
                    count,
                    percent
                });
            }
            return resultArr.sort((a, b) => a.count - b.count)
        }

        /**
         * 5.
         * +++ 我们知道：Excel表格的列是使用
         * A-Z的字母来表示列号的
         * 
         * 写一个方法，
         * 接受一个字符串形式的Excel列号，
         * 计算出该列号代表第几列，
         * 并将结果返回。
         * 
         * 比如A是第一列，所以方法接受A 输出1
         * B是第二列，方法接受B，输出2
         * Z是第26列，方法接受Z 输出26
         * AA是第27列，方法接受AA 输出27
         * ABCD是第19010列，方法接受ABCD，输出19010
         * 某某字符串是第n列，方法接受该字符串 应该输出n。
         * 就是要找到一个方法传入任意一串字母，然后计算出这个n
         * @param {string} text
         * @returns {number}
         */
        function convertExcelColumnCodeToNumber(text) {
            const str = text.toUpperCase();
            const strLength = text.length;
            let num = 0;
            for (let i = strLength - 1, j = 1; i >= 0; i--, j *= 26) {
                let char = str[i];
                // if (char < 'A' || char > 'Z') return 0;
                num += parseInt(parseInt(char.codePointAt() - 64) * j);
            }
            return num;
        }


        /**
         * @typedef {object} ITree
         * @property {string} name
         * @property {ITree[]} children
         */

        /**
         * 6.
         * +++ 有这样一个树形数据结构，
         * 根节点是一个对象，
         * 其中有一个属性name
         * 可能还有一个children属性，
         * 里面又包含同样的结构。
         * 层层递进，如果递进到某层没有
         * 这个children属性，
         * 或者children中个数为0，
         * 则说明到了叶子节点。
         * 
         * 可能根节点本身就是一个叶子
         * 
         * 写一个方法，
         * 接受一个这样的树形数据结果，
         * 收集出所有叶子节点的名字
         * 放到数组中, 返回该数组。
         * interface ITree {
         *  name: string,
         *  children: ITree[];
         * }
         * @param {ITree}
         * @returns {string[]}
         */
        function getAllLeafNames(tree) {
            const resultArr = [];
            const recurion = function (array) {
                for (let i = 0; i < array.length; i++) {
                    const node = array[i];
                    resultArr.push(node.name);
                    if (node.children && node.children.length > 0) {
                        recurion(node.children)
                    }
                }
            }
            if (!tree.children || tree.children.length === 0) {
                resultArr.push(tree.name);
            }
            if (tree.children && tree.children.length > 0) {
                resultArr.push(tree.name);
                recurion(tree.children);
            }

            return resultArr;
        }